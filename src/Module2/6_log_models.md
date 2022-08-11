
# Logging Models

## Saving Models

After we select the best model we can log whole models for storage (see Model Registry later), to do this we add a line at the end of our `with mlflow.start_run()` block:

```python
mlflow.<framework>.log_model(model, artifact_path="models_mlflow")
```

Where we replace the `<framework>` wih our model's framework (`sklearn`, `xgboost`, ... etc.).
The `artifact_path` defines where in the `artifact_uri` the model is stored.

We now have our model inside our `models_mlflow` directory in the experiment folder. 

**Note:** Using Autologging would store more data on parameters as well as the model. i.e: Use `log_model ` is redundant when using the autologger.

## Saving Artifacts with the Model

Sometimes we may want to save some artifacts with the model, for example in our case we may want to save the `DictVectorizer` object with the model for inference (subsequently testing as well). In that case we save the artifact as:
```python
mlflow.log_artifact("vectorizer.pkl", artifact_path = "extra_artifacts")
```

Where `vectorizer.pkl` is the vectorizer stored in a Pickle file and `extra_artifacts` the folder within the artifacts of the model where the file is stored.

An example of saving artifacts with the model:

```python
with mlflow.start_run():

    train = xgb.DMatrix(X_train, label=y_train)
    valid = xgb.DMatrix(X_val, label=y_val)
    
    best_params = {
        "learning_rate": 0.19000742747973715,
        "max_depth": 44,
        "min_child_weight": 3.852547711639823,
        "objective": "reg:linear",
        "reg_alpha": 0.006755095335696288,
        "reg_lambda": 0.1890415913639682,
        "seed":	42,
    }

    mlflow.log_params(best_params)

    booster = xgb.train(
                params=best_params,
                dtrain=train,
                num_boost_round=1000,
                evals=[(valid, 'validation')],
                early_stopping_rounds=50
            )

    y_pred = booster.predict(valid)
    rmse = mean_squared_error(y_val, y_pred, squared = False)
    mlflow.log_metric("rmse", rmse)

    with open("vectorizer.pkl", "wb") as f_out:
        pickle.dump(dv, f_out)
    
    mlflow.log_artifact("vectorizer.pkl", artifact_path = "extra_artifacts")
    mlflow.xgboost.log_model(booster, artifact_path = "models_mlflow")
```

## Loading Models:

We can use the model to make predictions with multiple ways depending on what we need:
+ We may load the model as a Spark UDF (User Defined Function) for use with Spark Dataframes
+ We may load the model as a MLflow PyFuncModel structure, to then use to predict data in a Pandas DataFrame, NumPy Array or SciPy Sparse Array. The obtained interface is general for all models from all frameworks
+ We may load the model as is, i.e: load the XGBoost model as an XGBoost model and treat it as such

The first two methods are explained briefly in the MLflow artifacts page for each run, for the latter we may use (XGBoost example):
```python
logged_model = 'runs:/9245396b47c94513bbf9a119b100aa47/models' # Model UUID from the MLflow Artifact page for the run

xgboost_model = mlflow.xgboost.load_model(logged_model)
```
The resultant `xgboost_model` is an XGBoost `Booster` object which behaves like any XGBoost model. We can predict as normal and even use XGBoost Booster functions such as `get_fscore` for feature importance.
