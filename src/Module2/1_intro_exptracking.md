# Introduction to Experiment tracking

## Important concepts

- **ML experiment:** the process of building an ML model; The whole process in which a Data Scientist creates and optimizes a model
- **Experiment run:** each trial in an ML experiment; Each run is within an ML experiment
- **Run artifact:** any file associated with an ML run: Examples include the model itself, package versions...etc; Each Artifact is tied to an Experiment
- **Experiment metadata:** metadata tied to each experiment



## Experiment tracking
Experiment tracking is the process of **keeping track of all the relevant information from an ML experiment**(relevant information depends on the experiment), which includes source code, environment, data, model, hyperparameters, metrics, etc.

Experiment tracking helps with:
- **Reproducibility**
- **Organization**
- **Optimization**

**Note:** Tracking experiments in spreadsheets helps but is not enough because **error prone**, **no standard format**, **no visibility and collaboration**.

## MLflow

![conda_logo](../Images/Module2/mlflow_logo.png)

*"An Open source platform for the machine learning lifecycle"*

Where ml lifecycle means the whole process of building and maintaining ml models. 

MLflow is a python package that contains four main modules:
- **Tracking**
- **Models**
- **Model registry**
- **Projects (Out of scope of this notes)**

You can check de official [MLflow Documentation](https://www.mlflow.org/docs/latest/index.html)

### Tracking experiments with MLflow:
The MLflow Tracking module allows you to organize your experiments into runs, and to keep track of:
- **Parameters:** Any parameter that affects the model like *hyperparameters*,  *training dataset path*, *preprocessing*, etc.
- **Metrics:** Metrics for training and test dataset
- **Metadata:** For example *tags*
- **Artifacts:** Any file like visualizations
- **Models**

Along with this information, MLflow automatically logs extra information about the run:
- **Source code**
- **Version of the code (git commit)**
- **Start and end time**
- **Author**
