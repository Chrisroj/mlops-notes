
# Autologging: 

Instead of logging the parameters by "Hand" by specifiying the logged parameters and passing them. We may use the Autologging feature in MLflow. There are two ways to use Autologging; First by enabling it globally in the code/Notebook using 
```python
mlflow.autolog()
```

or by enabling the framework-specific autologger, example with XGBoost:

```python
mlflow.xgboost.autolog()
```
Both must be done before running the experiments like. You can check the frameworks supported by autologger in [Automatic Logging](https://www.mlflow.org/docs/latest/tracking.html#automatic-logging)

An example of how to use autologging(We don't need `with mlflow.start_run():`) in MLflow is the next example belong to the best model selected:
```python
best_params = {
    "learning_rate": 0.19000742747973715,
    "max_depth": 44,
    "min_child_weight": 3.852547711639823,
    "objective": "reg:linear",
    "reg_alpha": 0.006755095335696288,
    "reg_lambda": 0.1890415913639682,
    "seed":	42,
}

mlflow.xgboost.autolog()

booster = xgb.train(
            params=best_params,
            dtrain=train,
            num_boost_round=1000,
            evals=[(valid, 'validation')],
            early_stopping_rounds=50
        )

```

The autologger then not only stores the model parameters for ease of use, it also stores other files inside the `model` (can be specified) folder inside our experiment artifact folder, these files include:
- `conda.yaml` and `requirements.txt`: Files which define the current envrionment for use with either `conda` or `pip` respectively
- `MLmodel` an internal MLflow file for organization
- Other framework-specific files such as the model itself