<img src = "https://bigdata.cs.ut.ee/smartml/images/banner.png">


[![DOI](http://joss.theoj.org/papers/10.21105/joss.00786/status.svg)](https://doi.org/10.5441/002/edbt.2019.54)


## SmartML: 
Curently, SmartML is an R-Package representing a meta learning-based framework for automated selection and hyperparameter tuning for machine learning algorithms. Being meta-learning based, the framework is able to simulate the role of the machine learning expert. In particular, the framework is equipped with a continuously updated knowledge base that stores information about the meta-features of all processed datasets along with the associated performance of the different classifiers and their tuned parameters. Thus, for any new dataset, SmartML automatically extracts its meta features and searches its knowledge base for the best performing algorithm to start its optimization process. In addition, SmartML makes use of the new runs to continuously enrich its knowledge base to improve its performance and robustness for future runs.

<img src = "https://bigdata.cs.ut.ee/smartml/images/arch.jpg">

---
## SmartML Contribution Points and Goals:

The goal of SmartML is to automate the process of classifier algorithm selection, and hyper-parameter tuning in supervised machine learning using a modified version of SMAC bayesian optimization that prefers explitation more than exploration thanks to Meta-Learning. 
1. SmartML is the first R package to deal with the sueprvised machine learning automation, and it is built over 16 different classifier algorithms from different R packages. <br>
2. In addition, we offer different data preprocessing, and feature engineering algorithms that can be specified by user and applied on tabular datasets of either CSV or ARFF extensions easily.
3. SmartML has a collaborative knowledge base that grows by time as more users are using our tool.
4. Finally, SmartML has the ability to do some model interpretability plots for feature importance and interaction by help of ```iml``` package for ML model interpretability.
5. SmartML has a web service interface for the demonstration purposes of the tool that can be found <b> <a href = "https://bigdata.cs.ut.ee/smartml/index.html"> HERE </a></b>.

---
## Installation

You can install the released version of SmartML from [Github](https://github.com/mmaher22/SmartML) with:

``` r
install_github("mmaher22/SmartML")
```

---
## User Manual

Manual for the SmartML R package can be found <a href = "https://github.com/mmaher22/Auto-Machine-Learning/blob/master/manual.pdf"> HERE </a>

---
## Example

This is a basic example which shows you how to run SmartML simply:

```{r}
library(SmartML)
```

```{r}
#' Option 1 = Classifier Selection Only, apply PCA as a preprocessing step with 4 components and get two candidate models as output only
result1 <- autoRLearn(1, 'sampleDatasets/shuttle/train.arff', 'sampleDatasets/shuttle/test.arff', option = 1, preProcessF = 'pca', nComp = 4, nModels = 2) 

#option 1 runs for Classifier Algorithm Selection Only
result1$clfs  #Vector of recommended nModels classifiers
result1$params #Vector of initial suggested parameter configurations of nModels recommended classifiers

#Use recommended model to train over training data and make predictions over test data
resultRun <- runClassifier(result1$TRData, result1$TEData, result1$params[[1]], result1$clfs[[1]])
resultRun$perf #model performance on test set
```

```{r}
#' Option 2 = Both Classifier Selection and Parameter Optimization and compute model interpretability plots
result2 <- autoRLearn(2, 'sampleDatasets/car/train.arff', 'sampleDatasets/car/test.arff', interp = TRUE) # Option 2 runs for both classifier algorithm selection and parameter tuning for 2 minutes.

result2$clfs #best classifier found
result2$params #parameter configuration for best classifier
result2$perf #performance of chosen classifier on testing set after fitting on whole training set
```

```{r}
plot(result2$interpret$featImp) #Feature Importance Plot
```

```{r}
#' Option 2 = Both Classifier Selection and Parameter Optimization, use 20% validation set from training set, and apply MICE for missing values imputation
result3 <- autoRLearn(5, 'sampleDatasets/EEGEyeState/train.csv', 'sampleDatasets/EEGEyeState/test.csv', vRatio = 0.2, missingOpr = TRUE) # Option 2 runs for both classifier algorithm selection and parameter tuning for 5 minutes.


result3$clfs #best classifier found
result3$params #parameter configuration for best classifier
result3$perf #performance of chosen classifier on testing set
```

---
## Contribution GuideLines to SmartML
To Contribute to `SmartML`, Please Follow these <a href = "https://github.com/mmaher22/SmartML/blob/master/CONTRIBUTE.md"> GuideLines </a>

---
## Publication

SmartML has been accepted as a DEMO paper at EDBT 19 in Lisbon Portugal <a href = "http://openproceedings.org/2019/conf/edbt/EDBT19_paper_235.pdf">[PDF]</a>:
```
Mohamed Maher, Sherif Sakr.,SMARTML: A Meta Learning-Based Framework for Automated Selection and Hyperparameter Tuning for Machine Learning Algorithms (2019). Advances in Database Technology-EDBT 2019: 22nd International Conference on Extending Database Technology, Lisbon, Portugal, March 26-29.
```

---
## Licence:
This work is licensed under the terms of the GNU General Public License, version 3.0 (GPLv3)
