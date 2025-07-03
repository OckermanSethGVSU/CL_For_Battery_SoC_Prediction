## Exploring Selective Continuous Learning for Battery State of Charge Prediction in Real-World Dynamic Charging Scenarios


This repo contains the code associated with the paper [Exploring Selective Continuous Learning for Battery State of Charge Prediction in Real-World Dynamic Charging Scenarios](https://doi.org/10.1016/j.jpowsour.2025.237418).

 This repo is a cleaned version of the code used in the paper, enabling easy reproducibility and future extensions. Feel free to modify use/modify the code for your specific use case. 


### Artifact Description

* `requirements.txt`: a list of the essential packages for running the notebooks.
* `full_env.txt`: a complete list of packages from the python environment used for testing in the paper.
* `data_prep.ipynb`: juypter notebook that downloads the necessary data and perform preprocessing with the [MIT dataset](https://data.matr.io/1/) used in this work.
* `main.ipynb`: juypter notebook that contains code to perform true-label fine-tuning and psuedo-label fine-tuning. 

* `preTrainedModels/`: this folder contains Pytorch files that allow you to load each model used in our work.

### Reproducibility
Below are the steps to reproduce our results. 

**1. Setup Python Env**

Our python environment contains packages that are not necessary to execute the notebook. We include it below as `full_env.txt` for completeness, but a more minimal option is included in `requirements.txt`.


Install only needed packages:

```
python3 -m venv batteryEnv
source batteryEnv/bin/activate
pip3 install -r envFiles/requirements.txt
```


Recreate our exact env: 

```
python3 -m venv batteryEnv
source batteryEnv/bin/activate
pip3 install -r envFiles/full_env.txt
```

Note that our code uses an older version of sklearn (1.3.2) where the `mean_squared_error` function has the deprecated `squared` keyword (producing RMSE instead of MSE). Newer versions of sklearn  `mean_squared_error` do not have this keyword. If you want to use a newer version, replace the `mean_squared_error` function in the code with the [`root_mean_squared_error`](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.root_mean_squared_error.html) function.


**2. Download and Preprocess MIT Dataset**

Execute the code in the `data_prep.ipynb` juypter notebook. The code preprocesses all the batteries in the MIT dataset, so it will take time to finish execution. All produced data will be contained with the `data` sub-directory within the active directory of the juypter notebook. 

**3. Execute driver code**

Within the `main.ipynb` file, there is code to:

* Define the model architectures
* Train the models from scratch
* Preload the models we used (if you do not want to train from scratch)
* Perform true-label fine-tuning and compare to the baseline models
* Perform psuedo-label fine-tuning using CL-WR and compare to the baseline models


The code includes comments and headers explaining its function. It is designed so that it can be easily modified if you want to try different training procedures, continous learning hyperparameters, or model architectures. 


### Citation

If any of our code was helpful to you or if you compare to our results, please consider citing us:


```
@article{Ockerman2025_Exploring,
title = {Exploring selective continuous learning for battery state of charge prediction in real-world dynamic charging scenarios},
journal = {Journal of Power Sources},
volume = {653},
pages = {237418},
year = {2025},
issn = {0378-7753},
doi = {https://doi.org/10.1016/j.jpowsour.2025.237418},
url = {https://www.sciencedirect.com/science/article/pii/S0378775325012546},
author = {Seth Ockerman and Olesia Elfimova and Harsh Sapra and Sage Kokjohn and Justin Shumaker and Shivaram Venkataraman},
keywords = {Capacity prediction, Fast-charging, State-of-charge prediction, Machine learning, Continuous learning},
}

```