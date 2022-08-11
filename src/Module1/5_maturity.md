# MLOps Maturity Model

[Video Source](https://www.youtube.com/watch?v=XwTH8BDGzYk&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK&index=7)

[Table Source](https://docs.microsoft.com/en-us/azure/architecture/example-scenario/mlops/mlops-maturity-model)

A framework for classifying different levels of MLOps maturity is listed below:


| Lvl |              | Overview | Use Case | 
|----:|--------------|----------|----------|  
| 0️⃣  | **No MLOps** | <ul><li>ML process highly manual</li><li>poor cooperation</li><li>lack of standards, success depends on an individual's expertise</li> </ul> | <ul><li>proof of concept (PoC)</li><li>academic project</li></ul> |
| 1️⃣  | **DevOps but no MLOps** | <ul><li>ML training is most often manual </li><li>software engineers might help with the deployment</li><li>automated tests and releases</li> </ul> | <ul><li>bringing PoC to production</li></ul> |
| 2️⃣  | **Automated Training** | <ul><li>ML experiment results are centrally tracked </li><li>training code and models are version controlled</li><li>deployment is handled by software engineers</li> </ul> | <ul><li>maintaining 2-3+ ML models</li></ul> |
| 3️⃣  | **Automated Model Deployment** | <ul><li>releases are managed by an automated CI/CD pipeline</li><li>close cooperation between data and software engineers</li><li>performance of the deployed model is monitored, A/B tests for model selection are used</li></ul> | <ul><li>business-critical ML services</li></ul> |
| 4️⃣  | **Full MLOps Automated Operations** | <ul><li>clearly defined metrics for model monitoring</li><li>automatic retraining triggered when passing a model metric's threshold</li> </ul>  | <ul><li>use only when a favorable trade-off between implementation cost and increase in efficiency is likely</li><li>retraining is needed often and is repetitive (has potential for automation)</li></ul> |

Be aware that not every project or even every part of a project needs to have the highest maturity level possible because it could exceed the project's resource budget. **Pragmatism is key**.