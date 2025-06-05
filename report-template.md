# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### NAME HERE

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
I realized the submission required only the "datetime" and "count" columns, so I had to ensure the predictions were placed into a copy of the test DataFrame and clipped to remove negative values before saving to CSV.

### What was the top ranked model that performed?
Initially, one of the LightGBM models (e.g., LightGBM/T2) was among the top-performing models with a root mean squared error (RMSE) of around -36.08.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
From the datetime column, new features such as `hour`, `dayofweek`, `month`, and `year` were extracted. These features were added to give the model more temporal context about usage patterns.

### How much better did your model preform after adding additional features and why do you think that is?
The model performance improved slightly after adding time-based features, with the RMSE improving from the initial score to approximately -35.8. The improvement likely came from better capturing hourly and weekly trends in bike usage.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
After using `presets="best_quality"` and allowing longer training time, the best model achieved an RMSE of -34.73. This was a clear improvement over the previous runs.

### If you were given more time with this dataset, where do you think you would spend more time?
I would spend more time on custom feature engineering (e.g., weather severity index), trying ensembling more models, and manually tuning the hyperparameters of top-performing models.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|hpo3|score|
|--|--|--|--|--|
|initial|default|none|none|~ 1.79 |
|add_features|added hour, dayofweek|added datetime parts|manual feature engineering|~ 1.80 |
|hpo|presets='best_quality'|600 sec training|LightGBM ensemble|1.81 |
|hpo|presets='medium_quality'|300 sec training|LightGBM ensemble|0.57 | --> because of memory error it is reduced

### Create a line plot showing the top model score for the three (or more) training runs during the project.

TODO: Replace the image below with your own. --> DONE

![model_train_score.png](img/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

TODO: Replace the image below with your own. --> DONE

![model_test_score.png](img/model_test_score.png)

## Summary
The AutoGluon framework was effective in building strong models quickly. By progressively adding features and tuning hyperparameters, the model's RMSE improved steadily. The top model used LightGBM with an ensemble strategy and benefited most from added time features and longer training time.
