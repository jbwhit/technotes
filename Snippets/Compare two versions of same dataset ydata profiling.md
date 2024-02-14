

https://docs.profiling.ydata.ai/latest/features/comparing_datasets/ 

```python
from ydata_profiling import ProfileReport

train_df = pd.read_csv("train.csv")
train_report = ProfileReport(train_df, title="Train")

test_df = pd.read_csv("test.csv")
test_report = ProfileReport(test_df, title="Test")

comparison_report = train_report.compare(test_report)
comparison_report.to_file("comparison.html")

```