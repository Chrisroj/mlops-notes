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

## Installing Miniconda from Terminal in Linux

Installing miniconda on Linux can be a bit tricky the first time you do it completely from the terminal. The following snippet will create a directory to install miniconda into, download the latest python 3 based install script for Linux 64 bit, run the install script, delete the install script, then add a conda initialize to your bash or zsh shell. After doing this you can restart your shell and conda will be ready to go.

```bash
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh

```
If you want to know how to do the same in macOS go to [install_miniconda_from_the_command_line](https://engineeringfordatascience.com/posts/install_miniconda_from_the_command_line/)

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