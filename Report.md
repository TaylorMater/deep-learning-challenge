## Overview of the analysis: 

The goal of this assignment was to investigate the creation and optimization of a neural network in classifying binary targets based off of a set of features. 

## Results:

----

### Data Preprocessing

What variable(s) are the target(s) for your model?

- The target variable was the IS_SUCCESSFUL column. 

What variable(s) are the features for your model? What variable(s) should be removed from the input data because they are neither targets nor features?


- We had more control over the features for the model. Some columns, like `'NAME'` and `'EIN'` were dropped because they had no baring on the target. But `'APPLICATION_TYPE'`, `'AFFILIATION'`, `'CLASSIFICATION'`, `'USE_CASE'`, `'ORGANIZATION'`, `'ASK_AMT'`, `'INCOME_AMT'`, `'SPECIAL_CONSIDERATIONS'`, and in some cases (dropped later for optimization purposes) `'STATUS'` were all used, albeit converted into separate numerical data columns via the `pd.get_dummies()`.


### Compiling, Training, and Evaluating the Model


How many neurons, layers, and activation functions did you select for your neural network model, and why? Were you able to achieve the target model performance? What steps did you take in your attempts to increase model performance?

- I set the initial input dimension to be the number of columns in the features (X) dataframe. I added a few more layers in the optimization stage to try to limit loss and increase the accuracy metric, but it didn't seem to help but only marginally. However, changing the activating functions from `relu` to `tanh` and `sigmoid` mainly lowered the accuracy, so I stuck with `relu` (excepting the `sigmoid` output layer). Adjusting the sizes of the number of neurons per layer, I was only able to have improvements on accuracy using a schema that was close to $70-50\%$ of the previous layer's neurons, until an eventual drop off from 9 to 1 in the output layer. I also changed the optimization method in the compilation to `SGM` instead of `adam`, which seemed to help some. Finally, I boosted the epochs up to 400 to see if that could boost accuracy more. I found that in the several attempts at optimizing, I couldn't really break the $~72.5\%$ barrier. It at least was about $1\%$ improvement from the default.

- I even tried increasing the amout of application types and classifications to try to have more information to pull from, but that didn't help too much, the $72.5\%$ convergence was still unavoidable. 

- Lastly, I tried to remove noise by removing the `Status` column completely and seeing if that would yield improvement, but it didn't impact things very much.




## Summary 

Summary: Summarize the overall results of the deep learning model. 

- My model could be better, but I worry about overfitting. More investigation into the different features, identifying more bin/fewer bins could likely help. Employing the use of an automatic optimization technique, where one defines a `create_model()` method that is then run over a selection of hyperparameters to create a best fit model probably would have yielded better results. A lot of my neuron/layer selection was trial and error, and this approach could have improved upon that and found more rigorous improvements. 