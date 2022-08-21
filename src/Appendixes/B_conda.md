# Conda Environments

![conda_logo](../Images/Appendixes/conda_logo.svg)


Conda is an open source package management system and environment management system that runs on Windows, macOS, Linux and z/OS. Conda quickly installs, runs and updates packages and their dependencies. Conda easily creates, saves, loads and switches between environments on your local computer. It was created for Python programs, but it can package and distribute software for any language.


**Note:** To manage Python resources on Mac M1 is recomendable to use **conda.** Using just pip is problematic for some python libraries if you use M1.

## Installing Conda

To install conda select the steps for your OS:


- [Windows](https://docs.conda.io/projects/conda/en/latest/user-guide/install/windows.html): Follow just the first 5 steps
- [macOS](https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html): Follow just the first 6 steps
- [Linux](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html): Follow just the first 6 steps

**Note:** You have to choose between install Miniconda or Anaconda. Miniconda is a free minimal installer for conda. It is a small, bootstrap version of Anaconda that includes only conda, Python, the packages they depend on, and a small number of other useful packages, including pip, zlib and a few others. **I prefer Miniconda than Anaconda**.

## Create an Environment

It's recommended to not install packages in `base`environment of `conda`, to create an independent environment type:

```bash
conda create --name ENVIRONMENT_NAME python=PYTHON_VERSION
```
Note: You can choose any python version you want, it will be installed if you don't have.

Example:

```bash
conda create --name exp-tracking-env python=3.9
```

To activate the environment type:

```bash
conda activate exp-tracking-env
```

To deactivate the environment

```bash
conda deactivate
```

## Jupyter Lab Setup

1. Install Jupyter Lab:
    
    ```bash
    conda install -c conda-forge jupyterlab
    ```
    
2. Add a conda environment:
    
    First activate the environment you want to add, second type:
    
    ```bash
    conda install ipykernel
    ```
    
    ```bash
    ipython kernel install --user --name=ENVIRONMENT_NAME
    ```
    

## Snippets

**Delete an environment**

```bash
conda remove --name ENVIRONMENT_NAME --all
```

**Show all environments**

```bash
conda info --envs
```
**Install libraries from a requirements.txt**

```bash
conda install --file requirements.txt
```

**Create `environment.yml` file via conda**

Inside your conda environment type:
```bash
 conda env export > environment.yml
```

**Create an environment from the `environment.yml` file**

```bash
conda env create -f environment.yml

```