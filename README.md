
[![CC BY-SA 4.0](https://img.shields.io/badge/License-CC_BY--SA_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

# Predicting Spotify Song Popularity: A Refactoring Journey

This lesson is part of the _Beyond Jupyter_ series, in which we address 
the specifics of software design in machine learning contexts.
We have put forth a set of [guiding principles](Guiding-Principles.md)
that can critically inform the decision-making process during development.

In the case study at hand, we will show how a machine learning use case that is implemented
as a Jupyter notebook (which was [taken from Kaggle](https://www.kaggle.com/code/sauravpalekar/spotify-song-popularity-prediction)) can be successively refactored in order to 
 * improve the software design in general, achieving a high degree clarity and maintainability,
 * gain flexibility for experimentation,
 * appropriately track results,
 * arrive at a solution that can straightforwardly be deployed for production.

The use case considers a dataset from kaggle containing meta-data on 
approximately one million songs (see download instructions below).
The goal is to use the data in order to learn a model for the prediction of song 
popularity given other song attributes such as the tempo, the release year, 
the key, the musical mode, etc.

## Preliminaries

In order for the code of each step to be runnable, set up a Python virtual environment
and download the Spotify song data.

### Python Environment

Use conda to create an environment based on [environment.yml](environment.yml) in the root folder of this repository:

    conda env create -f environment.yml

This will create a conda environment named `pop`.

### Configure Your IDE's Runtime Environment

Configure your IDE to use the `pop` environment created in the previous step.

### Downloading the Data

You can download the data in two ways:

 * Manually [download it from the Kaggle website](https://www.kaggle.com/datasets/amitanshjoshi/spotify-1million-tracks).
   Place the CSV file `spotify_data.csv` in the `data` folder (in the root of this repository).

   ![data_folder](resources/data_folder.png)

 * Alternatively, use the script [load_data.py](load_data.py) to automatically download the raw data CSV file to the subfolder
   `data` on the top level of the repository.
   Note that a Kaggle API key, which must be configured in `kaggle.json`, is required for this 
   (see [instructions](https://www.kaggle.com/docs/api)).


## How to use this package?

This package is organised as follows:
 * There is one folder per step in the refactoring process with a dedicated README file explaining the key aspects of the respective step.
 * There is an independent Python implementation of the use case in each folder, which you should inspect alongside the README file.  

The intended way of exploring this package is to clone the repository and open it in your IDE of choice, 
such that you can browse it with familiar tools and navigate the code efficiently.

### Diffing

To more clearly see the concrete changes from one step to another, you can make use 
of a diff tool. 
To support this, in folder `refactoring-journey/`, you may run the Python script 
`generate_repository.py` in order to create a git repository in folder `refactoring-repo` that references 
the state of each step in a separate tag, i.e. in said folder, you could run, for example,
   
        git difftool step04-refactoring step05-sensai


## Steps in the Journey

These are the steps of the journey:

 0. [Monolithic Notebook](refactoring-journey/step00-monolithic-notebook/README.md)
   
    This is the starting point, a Jupyter notebook which is largely unstructured.  
   
 1. [Python Script](refactoring-journey/step01-python-script/README.md)

    This step extracts the code that is strictly concerned with the training and evaluation of models.

 2. [Dataset Representation](refactoring-journey/step02-dataset-representation/README.md)

    This step introduces an explicit representation for the dataset, making transformations explicit as well as optional.

 3. [Model-Specific Pipelines](refactoring-journey/step03-model-specific-pipelines/README.md)

    This step refactors the pipeline to move all transforming operations into the models, enabling different models to use entirely different pipelines.

 4. [Refactoring](refactoring-journey/step04-refactoring/README.md)

    This step improves the code structure by adding function-specific Python modules.

 5. [sensAI](refactoring-journey/step05-sensai/README.md)

    This step introduces the high-level library sensAI, which will enable more flexible, declarative model specifications down the line.
    It furthermore facilitates logging, model evaluation and helps with other minor details.

 6. [Feature Representation](refactoring-journey/step06-feature-representation/README.md)

    This step separates representations of features and their properties from the models that use them, allowing
    model input pipelines to be flexibly composed.

 7. [Feature Engineering](refactoring-journey/step07-feature-engineering/README.md)

    This step adds an engineered feature to the mix.

 8. [Tracking Experiments](refactoring-journey/step08-tracking-experiments/README.md)

    This step adds tracking functionality via sensAI's mlflow integration and by logging directly to the file system.

 9. [Regression](refactoring-journey/step09-regression/README.md)

    This step considers the perhaps more natural formulation of the prediction problem as a regression problem.

10. [Hyperparameter Optimisation](refactoring-journey/step10-hyperopt/README.md)

    This step adds hyperparameter optimisation for the XGBoost regression model.

11. [Cross-Validation](refactoring-journey/step11-cross-validation/README.md)

    This step adds the option to use cross-validation.

12. [Deployment](refactoring-journey/step12-deployment/README.md)

    This step adds a web service for inference, which is packaged in a docker container.

