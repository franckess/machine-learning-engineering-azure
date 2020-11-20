## Project Overview

In this project, you'll have the opportunity to create and optimize an ML pipeline. You'll be provided a custom-coded model—a standard Scikit-learn Logistic Regression—the hyperparameters of which you will optimize using HyperDrive. You'll also use AutoML to build and optimize a model on the same dataset, so that you can compare the results of the two methods.

You can see the main steps that you'll be taking in the diagram below:
[alt text](Image/creating-and-optimizing-an-ml-pipeline.png)

## Steps to complete the project

### Getting started

- [ ] Clone the [GitHub repository](https://github.com/udacity/nd00333_AZMLND_Optimizing_a_Pipeline_in_Azure-Starter_Files)
- [ ] Open the "Azure Workspace" page in the classroom
- [ ] Access lab via virtual machine
- [ ] Once the virtual machine has loaded, open browser, navigate to Github and log in
- [ ] Log into Azure portal, navigate to "ml.azure.com"
- [ ] Access the Azure Machine Learning Workspace
- [ ] Navigate to the "Notebooks" page
- [ ] Click "Upload files" and upload your notebook and the `train.py` script to Azure

### Setting up training script

Review and modify the `train.py` script to run in your pipeline.

- [ ] Read through the training script to ensure a good understanding
- [ ] Identify/check for parameters you may need to pass to the script later
- [ ] Import the data from the specified URL using `TabularDatasetFactory`
- [ ] Split data into _train_ and _test_ sets

### HyperDrive pipeline

In this step, we'll build our training pipeline. We'll start by getting the workspace and experiment objects running. Then, you'll build your pipeline—from creating a compute cluster, to HyperDrive, to running the train.py script containing the custom-coded Logistic Regression with a HyperDrive run.

- [ ] Create a compute cluster to run the experiment on using `"Standard_D2_V2"`
- [ ] Specify a parameter sampler
- [ ] Specify a policy for early stopping
- [ ] Create an estimator for the `train.py` script
- [ ] Create a HyperDrive
- [ ] Submit the HyperDriveConfig to run the experiment
- [ ] Use the RunDetails widget to see the progress of your run
- [ ] Use the `.get_best_run_by_primary_metric()` method of the run to select the best hyperparameter for your model
- [ ] Save your model

### AutoML Run

Once you've completed your HyperDrive run (or while it is running!), you can set up your AutoMLConfig in the same Notebook. In this section, you'll import your data from the specified URL again, clean the data, and pass the cleaned data to an AutoMLConfig that you create.

But be careful with your configuration: **Your AutoML instances will time out after 30 minutes!**

- [ ] Create a dataset from the provided URL using `TabularDatasetFactory` in the notebook
- [ ] Split data into train and test sets
- [ ] Modify the provided AutoML config
- [ ] Submit your AutoML
- [ ] Save the best model

### Modifying the README

- [ ] A summary of the problem statement
- [ ] How the problem solved
- [ ] Explanation of the architecture, data, hyperparameters, and classification algorithm
- [ ] Explanation of the rationale for choosing a particular parameter
- [ ] Explanation of the rationale for choosing a particular early stopping policy
- [ ] Description of the model and hyperparameters produced by AutoML
- [ ] Comparison of the models and their performance
- [ ] Identification of areas to improve the outcome
- [ ] (Optional) Proof of cluster cleanup if not included in the notebook

### Commit to your Github


