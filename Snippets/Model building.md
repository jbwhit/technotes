

```python
import numpy as np
import pandas as pd
from sklearn.model_selection import cross_val_score, KFold, train_test_split, learning_curve, validation_curve
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.linear_model import LogisticRegression
import xgboost as xgb
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix, roc_auc_score
import matplotlib.pyplot as plt
import seaborn as sns

def create_feature_pipeline():
    """Create a preprocessing pipeline for feature transformation."""
    numeric_features = ['age', 'income', 'tenure']
    categorical_features = ['education', 'occupation', 'location']
    
    numeric_transformer = Pipeline(steps=[
        ('scaler', StandardScaler())
    ])
    
    categorical_transformer = Pipeline(steps=[
        ('onehot', OneHotEncoder(drop='first', sparse_output=False))
    ])
    
    preprocessor = ColumnTransformer(
        transformers=[
            ('num', numeric_transformer, numeric_features),
            ('cat', categorical_transformer, categorical_features)
        ])
    
    return preprocessor

def build_model_pipelines():
    """Create pipelines for individual models."""
    preprocessor = create_feature_pipeline()
    
    # Logistic Regression pipeline
    lr_pipeline = Pipeline([
        ('preprocessor', preprocessor),
        ('classifier', LogisticRegression(random_state=42))
    ])
    
    # XGBoost pipeline
    xgb_pipeline = Pipeline([
        ('preprocessor', preprocessor),
        ('classifier', xgb.XGBClassifier(random_state=42))
    ])
    
    return {
        'logistic': lr_pipeline,
        'xgboost': xgb_pipeline
    }

def evaluate_model(y_true, y_pred, y_prob, model_name):
    """Evaluate model performance with multiple metrics."""
    print(f"\n{'-'*20} {model_name} Evaluation {'-'*20}")
    print("\nClassification Report:")
    print(classification_report(y_true, y_pred))
    
    print("\nConfusion Matrix:")
    cm = confusion_matrix(y_true, y_pred)
    print(cm)
    
    # Plot confusion matrix
    plt.figure(figsize=(8, 6))
    sns.heatmap(cm, annot=True, fmt='d', cmap='Blues')
    plt.title(f'Confusion Matrix - {model_name}')
    plt.ylabel('True Label')
    plt.xlabel('Predicted Label')
    plt.show()
    
    # Calculate ROC AUC
    roc_auc = roc_auc_score(y_true, y_prob)
    print(f"\nROC AUC Score: {roc_auc:.3f}")

def create_ensemble_predictions(model_predictions, model_probas):
    """Create ensemble predictions using weighted voting."""
    # Use ROC AUC scores as weights
    weights = []
    for model_name, y_pred in model_predictions.items():
        roc_auc = roc_auc_score(y_test, model_probas[model_name])
        weights.append(roc_auc)
    
    # Normalize weights
    weights = np.array(weights) / sum(weights)
    
    # Create weighted average of probabilities
    ensemble_proba = np.zeros_like(model_probas[list(model_probas.keys())[0]])
    for (model_name, proba), weight in zip(model_probas.items(), weights):
        ensemble_proba += weight * proba
    
    ensemble_pred = ensemble_proba > 0.5
    return ensemble_pred, ensemble_proba

# Generate data
df = generate_customer_data(n_samples=1000, random_state=42)

# Split features and target
X = df.drop('churn', axis=1)
y = df['churn']

# Create train/test split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Build model pipelines
pipelines = build_model_pipelines()

# Perform cross-validation for each model
print("\nCross-validation Results:")
cv = KFold(n_splits=5, shuffle=True, random_state=42)
for name, pipeline in pipelines.items():
    cv_scores = cross_val_score(pipeline, X_train, y_train, cv=cv, scoring='roc_auc')
    print(f"\n{name}:")
    print(f"Mean ROC AUC: {cv_scores.mean():.3f} (+/- {cv_scores.std() * 2:.3f})")

# Train final models and make predictions
model_predictions = {}
model_probas = {}

for name, pipeline in pipelines.items():
    # Fit model
    pipeline.fit(X_train, y_train)
    
    # Make predictions
    y_pred = pipeline.predict(X_test)
    y_prob = pipeline.predict_proba(X_test)[:, 1]
    
    # Store predictions
    model_predictions[name] = y_pred
    model_probas[name] = y_prob
    
    # Evaluate individual model
    evaluate_model(y_test, y_pred, y_prob, name)

# Create and evaluate ensemble
ensemble_pred, ensemble_proba = create_ensemble_predictions(model_predictions, model_probas)
evaluate_model(y_test, ensemble_pred, ensemble_proba, "Weighted Ensemble")

# Feature importance analysis for XGBoost
xgb_pipeline = pipelines['xgboost']
feature_names = (
    ['age', 'income', 'tenure'] + 
    [f"{feature}_{val}" for feature, vals in 
     zip(['education', 'occupation', 'location'], 
         xgb_pipeline.named_steps['preprocessor']
         .named_transformers_['cat']
         .named_steps['onehot']
         .categories_)
     for val in vals[1:]]
)

xgb_importance = xgb_pipeline.named_steps['classifier'].feature_importances_
importance_df = pd.DataFrame({
    'feature': feature_names,
    'importance': xgb_importance
}).sort_values('importance', ascending=False)

plt.figure(figsize=(10, 6))
sns.barplot(data=importance_df.head(10), x='importance', y='feature')
plt.title('Top 10 Most Important Features (XGBoost)')
plt.show()
```