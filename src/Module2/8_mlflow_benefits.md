# MLflow: Benefits, Limitations and Alternatives

## Tracking benefits:
- The tracking server can be easily deployed to the cloud
- Share experiments with other data scientists
- Collaborate with others to build and deploy models
- Give more visibility of the data science efforts

## Issues with running a remote (shared) MLflow server
- **Security:**  
    - Restrict access to the server (e.g. access through VPN) to avoid people outside your organization may get acces to the experiments, runs, models, etc.

- **Scalability:**

    - Check [Deploy MLflow on AWS Fargate](https://github.com/aws-samples/amazon-sagemaker-mlflow-fargate) scale nicely when the number of users that access(to the mlflow server) increases.

    - Check [MLflow at Company Scale by Jean-Denis Lesage](https://www.databricks.com/session_eu20/mlflow-at-company-scale) to scale mlflow to be able to support thousands of experiments runs and also models.

- **Isolation**
    - Define standard for naming experiments, models and a set of default tags(developer or team name as a tag)
    - Restrict access to artifacts (e.g. use s3 buckets living in different AWS accounts)


## MLflow limitations (and when not to use it)
- **Authentication & Users:** The open source version of MLflow doesn’t provide
any sort of authentication.
- **Data versioning:** to ensure full reproducibility we need to version the data
used to train the model. MLflow doesn’t provide a built-in solution for that but
there are a few ways to deal with this limitation
- **Model/Data Monitoring & Alerting:** this is outside of the scope of MLflow
and currently there are more suitable tools for doing this

## MLflow alternatives

There are some paid alternatives to MLflow:
- [Neptune](https://neptune.ai/)
- [Comet](https://www.comet.com/site/)
- [Weights & Biases](https://wandb.ai/site)
- You can go to [many more](https://neptune.ai/blog/best-ml-experiment-tracking-tools) to see a detailed comparation