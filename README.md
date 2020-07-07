# Anaconda Note

## Getting Started

This guide is loosely followed this [cheat sheet](https://conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf). As soon as you finished installing Anaconda, update your packages by running 

```python
conda update conda 
conda update anaconda
```

This will update all the packages and conda itself if it is necessary. 



## Creating an environment

If you are working on the multiple projects with different configurations, it is good to have a python environment for each project. There are other projects like `virtualenv` but as a data scientist, we always come back to `Anaconda` since it is very easy and reliable. If you need to scale up to AWS , Azure or Google Compute, you can still get a docker container for `mini-conda` which is the light weighted version of `Anaconda`. 

There are multiple way to create the working environments. 

For **local usage**,

```python
conda create --name myenv #create your environment named 'myenv'
conda activate myenv #then activate my environment
conda deactive # this will deactivate your current environment
```

When you install `Anaconda`, it will come with the `base` environment.  For instance if you want to clone the new environment from the current working environment, you can do so by `conda create --name myNewEnv --clone myenv` . This will clone a new environment named `myNewEnv` from `myenv`.  Or you can replace `myenv` with `base`  to clone from the base environment. 



For **deployment** to the cloud, I would recommend `yml` file. Here is the sample of `yml` file:

```yml
name: sample
channels:
  - defaults
  - conda-forge
  - file:///user/localchannel

dependencies:
  - python=3.7
  - scikit-learn=0.23.*
  - lightgbm=2.3.*
  - numpy
  - pandas
  - sqlalchemy
  - pip
  - pip:
  - jupyterlab
  - joblib

```

Sometimes you could not find the libraries/packages in conda `defaults` channel. Then another popular palce is `conda-forge` . You could also add your own personal libraries if you package it with `conda`. 

Then you just point the location like `- file:///user/channel` if your channel is `/user/channel`. This is similar to the packages with the url link. The default channel_alias for anaconda is http://conda.anaconda.org/.

To use `yml` file, run 

`conda create --name newEnv --file=youfile1.yml --file=yourfile2.yml`

## Checking/Deleting Environment

If you want to get all the names of environment, run `conda list`.  To delete the environment after you finish your project, run `conda remove --name yourOldEnv --all`. 

## Search Packages

You can search packages by `conda search pip=20.2` . This will search `pip` in the default conda channel. You can also specify the channel by `conda search -c conda-forge pip=20` . This will search the package in `conda-forge` channel. `conda-forge` is a very popular conda channel. Some companies have their own conda channel (e.g. `install pytorch torchvision -c pytorch`) . 



## Exporting your environment

To share your environment, run `conda env export --name yourEnv > environment.yml` to save your environment in `environment.yml` file.