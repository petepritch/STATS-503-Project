# STATS-503-Project
This project is for partial credit of STATS 503 Multivariate Analysis @ The University of Michigan, Ann Arbor.

## Guidelines

This project is an opportunity to apply the statistical learning techniques covered in class to a real dataset. The project has two parts. The first part is a somewhat open-ended investigation: you will pose and answer two questions using data from the National Health and Nutrition Examination Survey (NHANES). The second part is a Kaggle competition: you will test your ability to build powerful predictive models. You will submit final reports detailing your analysis.

## NHANES Report Abstract

We investigate the presence of volatile organic compounds (VOCs) in human blood samples and
their relationship with various levels of exposure to tobacco products. Our analysis demonstrates
that, while not as significant as might be expected, there is a significant relationship between
VOC concentrations and exposure levels. By analyzing the results from our models, we also can
draw conclusions about the difference in effect between second-hand and direct tobacco usage.
We accomplish this objective by leveraging interpretable statistical learning models and thorough
analysis of data.

------

## Kaggle Report

Click [here](https://www.kaggle.com/competitions/stats-503-final-project-winter-2024) to view the competition on Kaggle.

In this report, we present our methods and models used to predict final student scores based on student retention predictors and various performance scores. Our main contributions include feature engineering tricks, multilayer perceptrons, and hyperparameter tuning. We also explain how bagging can be harnessed to improve variance in the final estimators. 

### Methods

The dataset consisted of a large number of weak, albeit independent predictors. This immediately creates a dimensionality issue, but the lack of any correlation between features makes dimensionality reduction intractable, as most known techniques rely on the assumption that the data lives in some lower-dimensional manifold. While we gave up on projecting the data into a lower-dimensional space, we realized that the key to success might be combining the features into a handful of more variable predictors. One easy way to do this was to sum all the retention features into a single retention score. This creates a single feature that accounts for a substantial amount of variability within the data set. We also combined student evaluation and teacher evaluation scores into a single score. With these new features, we were able to achieve an estimated R^2 of around .85 even with just simple models like ridge-regression. 

Subsequently, we focused on improving the strength of the models we used. We first experimented with advanced boosting methods, which generally perform exceptionally well on tabular data. The results were satisfactory, achieving an R^2 of roughly .87. However, we were convinced we could grind out a few more decimal places, and finding the right parameters was incredibly challenging. So, we jumped straight into the deep end with simple FC networks. Since there was not a lot of data, we wanted to be conservative with the size of the model, so we used the multi-layer perceptron with one hidden layer and 64 hidden units. Due to the simplicity of the architecture, we used scikit-learn modules to implement this, as higher-level deep-learning frameworks were not needed. We used cross-validation to tune the parameters and found that sigmoid activation and Newtonian-based optimization methods worked best, and we trained till convergence. Since the network was small, we didn’t have issues with overfitting. However, we did bag 30 MLP models in the end, as this had a slight improvement in overall R^2, (but only to the tune of about .01). This was our final model, and it achieved a private leaderboard score of 0.88995.

With additional time, it would have been both educational and interesting to test additional models in a different fully featured DL framework such as PyTorch. Moreover, we would have liked to see if ensemble methods such as stacking and voting various models are able to hold a candle to our final model. 

### Member Contributions

- Pete: Pete did most of the initial data analysis, which helped us analyze what wasn’t working and how to build the right features. Pete also worked on designing the models that we used. 
- Omar: Primarily worked on implementing the features that work suggested from Pete’s analysis as well as designing and optimizing the models. Architecture. 
- Pan: Worked on both data analysis and model design, as well as testing various alternative models like boosted regression trees and adaptive boosting.  We all contributed evenly to writing the report. 

