## Lesson Outline: AutoML and Hyperparameter Tuning
In this lesson, we'll see how we can use Automated ML and Hyperparameter tuning to dramatically speed up the development of our models. Here's what we'll be covering:

* **Automated ML and SDK.** We'll discuss how we can use the Azure ML SDK with AutoML to operationalize and automate model creation—allowing you to create models more quickly and accurately.
* **Model Interpretation.** We'll explore how model interpretation allows us to build solutions using AutoML that we (and others) can more easily interpret, making visible the core features that are driving the model.
* **Exporting Models with ONNX.** ONNX is a portability platform for models that was created by Microsoft and that allows you to convert models from one framework to another, or even to deploy models to a device (such as an iOS or Android mobile device).

### Hyperparameter Tuning with HyperDrive

Main steps for tuning with hyperDrive

* **Define the parameter search space.** This could be a discrete/categorical variable (e.g., apple, banana, pair) or it can be a continuous value (e.g., a time series value).
* **Define the sampling method over the search space.** This is a question of the method you want to use to find the values. For example, you can use a random, grid, or Bayesian search strategy.
* **Specify the primary metric to optimize.** For example, the Area Under the Curve (AUC) is a common optimization metric.
* **Define an early termination policy.** An early termination policy specifies that if you have a certain number of failures, HyperDrive will stop looking for the answer.

You can control HyperDrive with the SDK as follows:
```python
from azureml.train.hyperdrive import BayesianParameterSampling
from azureml.train.hyperdrive import uniform, choice
param_sampling = BayesianParameterSampling( {
        "learning_rate": uniform(0.05, 0.1),
        "batch_size": choice(16, 32, 64, 128)
    }
)
```
Wwe can also tune any type of variables:
```python
## Discrete variables
{
    "batch_size": choice(16, 32, 64, 128)
    "number_of_hidden_layers": choice(range(1,5))
    }

## Continuous variables
{    
    "learning_rate": normal(10, 3),
    "keep_probability": uniform(0.05, 0.1)
    }
```
We can also pull out relevant results from our experiment as follows:
```python
best_run = hyperdrive_run.get_best_run_by_primary_metric()
best_run_metrics = best_run.get_metrics()
parameter_values = best_run.get_details()['runDefinition']['Arguments']

print('Best Run Id: ', best_run.id)
print('\n Accuracy:', best_run_metrics['accuracy'])
print('\n learning rate:',parameter_values[3])
print('\n keep probability:',parameter_values[5])
print('\n batch size:',parameter_values[7])
```

### Automatic ML and the SDK

To understand why Automated ML is a useful tool, it helps to first understand some of the challenges we face with traditional ML. These include:

* **Focus on technical details vs the business problem.** The code and technical details can consume large amounts of the available resources, distracting our focus from the business problem we want to use the ML to solve.
* **Lack of automation.** With traditional ML, we have to do many things manually, even though they could easily be automated with tools like Azure ML Studio.
* **Too much HiPPO influence.** The Highest Paid Person's Opinion (HiPPO) can have an unduly large influence on decisions about the output of the model, even though this decision might be better made automatically.
* **Feature engineering.** What are the features that I need to get the best accuracy? What are the columns I should select? This can be a huge task that requires a lot of human effort.
* **Hyperparameter selection.** For example, with a clustering model, what number of clusters will give the best results? There can be a lot of trial and error and many false starts.
* **Training and Tuning.** What are the different parameters you're using when training your model? What machines and resources should you use? How should you best tune the parameters? In traditional ML, these questions require a human to supervise the process.

#### Automated ML

Automated ML can help with all of the above problems. Essentially, AutoML involves the application of DevOps principles to machine learning, in order to automate all aspects of the process. For example, we can automate feature engineering, hyperparameter selection, model training, and tuning. With AutoML, we can:

* Create hundreds of models a day
* Get better model accuracy
* Deploy models faster

This creates a quicker feedback loop and allows us to bring ideas to market much sooner. Overall, it reduces the time that we have to spend on technical details, allowing for more effort to be put into solving the underlying business problems.

#### Configuring AutoML from the SDK

We can easily leverage AutoML from the SDK to automate many aspects of our pipeline, including:

* Task type
* Algorithm iterations
* Accuracy metric to optimize
* Algorithms to blacklist/whitelist
* Number of cross-validations
* Compute targets
* Training data

To do this, we first use the `AutoMLConfig` class. In the code example below, you can see that we are creating an `automl_config` object and setting many of the parameters listed above:
```python
from azureml.train.automl import AutoMLConfig

automl_config = AutoMLConfig(task="classification",
                             X=your_training_features,
                             y=your_training_labels,
                             iterations=30,
                             iteration_timeout_minutes=5,
                             primary_metric="AUC_weighted",
                             n_cross_validations=5
                            )
```

#### Running AutoML from the SDK

Once we have completed our configuration, we can then run it using the SDK. Here's a typical example of what that would look like:
```python
from azureml.core.experiment import Experiment

experiment = Experiment(ws, "automl_test_experiment")
run = experiment.submit(config=automl_config, show_output=True)
```

### ONNX (Open Neural Network Exchange)

The [Open Neural Network Exchange (ONNX)](https://onnx.ai/) is an open-sources portability platform for models that allows you to convert models from one framework to another, or even to deploy models to a device (such as an iOS or Android mobile device).

To get models running with ONNX, several options are provided:

* Train the model in Azure ML
* Convert existing model
* Get a pre-trained ONNX model
* Create  an ONNX model from an AutoML service, such as Azure Custom Vision service

#### Using the Runtime

Installation can be done with a simple pip install, for either CPU or GPU builds:
```python
pip install onnxruntime       # CPU build
pip install onnxruntime-gpu   # GPU build
```
Then we can simply import the runtime and then instantiate an `InferenceSession` object, passing in the path to the model:
```python
import onnxruntime
session = onnxruntime.InferenceSession("path to model")
```

#### Practicing with ONNX

Below is a sample code to practice ONNX in Jupyter Notebook

* First we download the CoreML model. We use the CoreML model from [Matthijs Hollemans's tutorial](https://github.com/hollance/YOLO-CoreML-MPSNNGraph).
```python
import urllib.request

coreml_model_url = "https://github.com/hollance/YOLO-CoreML-MPSNNGraph/raw/master/TinyYOLO-CoreML/TinyYOLO-CoreML/TinyYOLO.mlmodel"
urllib.request.urlretrieve(coreml_model_url, filename="TinyYOLO.mlmodel")
```

* Then we download/use ONNXMLTools to convert the model.
```python
## Download relevant libraries
!pip install onnxmltools
!pip install coremltools

## Import libraries
import onnxmltools
import coremltools
```

* Load a CoreML model
```python
coreml_model = coremltools.utils.load_spec('TinyYOLO.mlmodel')
```

* Convert from CoreML into ONNX
```python
onnx_model = onnxmltools.convert_coreml(coreml_model, 'TinyYOLOv2')
```

* Save ONNX model
```python
onnxmltools.utils.save_model(onnx_model, 'tinyyolov2.onnx')
```

* Get the size
```python
import os
print(os.path.getsize('tinyyolov2.onnx'))
```



