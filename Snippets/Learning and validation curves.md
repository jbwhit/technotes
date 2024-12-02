
```python
import numpy as np
import pandas as pd
from sklearn.model_selection import learning_curve, validation_curve
import matplotlib.pyplot as plt
import seaborn as sns

def plot_learning_curves(estimator, X, y, title, cv=5):
    """
    Plot learning curves to diagnose bias/variance tradeoff.
    
    Parameters:
    -----------
    estimator : sklearn estimator object
        The model pipeline to evaluate
    X : array-like
        Training data
    y : array-like
        Target values
    title : str
        Title for the plot
    cv : int
        Number of cross-validation folds
    """
    # Set up plot style
    plt.style.use('seaborn')
    fig, ax = plt.subplots(figsize=(10, 6))
    
    # Calculate learning curves
    train_sizes = np.linspace(0.1, 1.0, 10)
    train_sizes, train_scores, val_scores = learning_curve(
        estimator,
        X, y,
        train_sizes=train_sizes,
        cv=cv,
        n_jobs=-1,
        scoring='roc_auc'
    )
    
    # Calculate mean and std
    train_mean = np.mean(train_scores, axis=1)
    train_std = np.std(train_scores, axis=1)
    val_mean = np.mean(val_scores, axis=1)
    val_std = np.std(val_scores, axis=1)
    
    # Plot learning curves
    ax.plot(train_sizes, train_mean, label='Training score', color='blue', marker='o')
    ax.fill_between(train_sizes, train_mean - train_std, train_mean + train_std, alpha=0.15, color='blue')
    
    ax.plot(train_sizes, val_mean, label='Cross-validation score', color='green', marker='o')
    ax.fill_between(train_sizes, val_mean - val_std, val_mean + val_std, alpha=0.15, color='green')
    
    # Customize plot
    ax.set_xlabel('Training Examples')
    ax.set_ylabel('ROC AUC Score')
    ax.set_title(f'Learning Curves - {title}')
    ax.legend(loc='lower right')
    ax.grid(True)
    
    # Add bias-variance analysis
    gap = train_mean[-1] - val_mean[-1]
    final_val_score = val_mean[-1]
    
    analysis_text = f"""
    Model Analysis:
    - Final validation score: {final_val_score:.3f}
    - Train-test gap: {gap:.3f}
    - Diagnosis: {diagnose_model(final_val_score, gap)}
    """
    
    plt.figtext(0.02, 0.02, analysis_text, fontsize=8, bbox=dict(facecolor='white', alpha=0.8))
    plt.tight_layout()
    plt.show()

def plot_validation_curves(estimator, X, y, param_name, param_range, title, cv=5):
    """
    Plot validation curves for a specific parameter.
    
    Parameters:
    -----------
    estimator : sklearn estimator object
        The model pipeline to evaluate
    X : array-like
        Training data
    y : array-like
        Target values
    param_name : str
        Name of the parameter to vary
    param_range : array-like
        Range of parameter values to test
    title : str
        Title for the plot
    cv : int
        Number of cross-validation folds
    """
    plt.style.use('seaborn')
    fig, ax = plt.subplots(figsize=(10, 6))
    
    # Calculate validation curves
    train_scores, val_scores = validation_curve(
        estimator,
        X, y,
        param_name=param_name,
        param_range=param_range,
        cv=cv,
        scoring='roc_auc',
        n_jobs=-1
    )
    
    # Calculate mean and std
    train_mean = np.mean(train_scores, axis=1)
    train_std = np.std(train_scores, axis=1)
    val_mean = np.mean(val_scores, axis=1)
    val_std = np.std(val_scores, axis=1)
    
    # Plot validation curves
    ax.plot(param_range, train_mean, label='Training score', color='blue', marker='o')
    ax.fill_between(param_range, train_mean - train_std, train_mean + train_std, alpha=0.15, color='blue')
    
    ax.plot(param_range, val_mean, label='Cross-validation score', color='green', marker='o')
    ax.fill_between(param_range, val_mean - val_std, val_mean + val_std, alpha=0.15, color='green')
    
    # Customize plot
    ax.set_xlabel(param_name)
    ax.set_ylabel('ROC AUC Score')
    ax.set_title(f'Validation Curves - {title}')
    ax.legend(loc='best')
    ax.grid(True)
    
    # Find optimal parameter value
    optimal_idx = np.argmax(val_mean)
    optimal_param = param_range[optimal_idx]
    optimal_score = val_mean[optimal_idx]
    
    analysis_text = f"""
    Parameter Analysis:
    - Optimal {param_name}: {optimal_param}
    - Best validation score: {optimal_score:.3f}
    """
    
    plt.figtext(0.02, 0.02, analysis_text, fontsize=8, bbox=dict(facecolor='white', alpha=0.8))
    plt.tight_layout()
    plt.show()

def diagnose_model(val_score, gap):
    """
    Provide diagnosis based on validation score and train-test gap.
    """
    if val_score < 0.6:
        if gap < 0.1:
            return "High Bias (Underfitting): Model is too simple"
        else:
            return "High Bias and High Variance: Model needs restructuring"
    else:
        if gap > 0.1:
            return "High Variance (Overfitting): Consider regularization or more training data"
        else:
            return "Good Fit: Model shows good balance"

# Example usage after training models
def perform_model_diagnostics(best_models, X_train, X_test, y_train, y_test):
    """
    Perform diagnostic analysis on trained models.
    """
    for name, model in best_models.items():
        print(f"\nPerforming diagnostics for {name}...")
        
        # Plot learning curves
        plot_learning_curves(model, X_train, y_train, name)
        
        # Plot validation curves for specific parameters
        if name == 'logistic':
            C_range = np.logspace(-3, 3, 7)
            plot_validation_curves(
                model, X_train, y_train,
                'classifier__C', C_range,
                f'{name} - Regularization Strength'
            )
        elif name == 'xgboost':
            depth_range = np.array([3, 4, 5, 6, 7, 8, 9])
            plot_validation_curves(
                model, X_train, y_train,
                'classifier__max_depth', depth_range,
                f'{name} - Max Depth'
            )

# Add this to your main execution
if __name__ == "__main__":
    # ... (previous code remains the same)
    
    # After training models, add:
    print("\nPerforming model diagnostics...")
    perform_model_diagnostics(best_models, X_train, X_test, y_train, y_test)
```