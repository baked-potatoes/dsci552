### AI Use Log

#### Prompt:

I've attached my Homework 5 assignment PDF and notebook template for context. Can you help me work through the problems and the ISLR questions? For each part, explain the steps and include the relevant Python code with suggested variable names, plus the written answers, so I can run and test everything myself on the data.

(Uploaded Homework4.pdf and bagai_sanchit_HW4.ipynb for context)

#### Response:

I'll go through the assignment section by section, explaining the relevant concepts, implementation approaches, and how to interpret the results.

### 1(a) Obtain Data

Start by loading the dataset using `pd.read_csv`. Since the file uses UTF-16 encoding, tab-separated values, and commas as decimal separators, specify these parameters explicitly.

Assign the column names and convert the yes/no target values into binary labels. Check the shape, data types, and first few rows before continuing.

### 1(b) Build a Decision Tree

Since there are two binary target variables, one approach is to combine them into a single multiclass target using the label powerset method.

You can then train a `DecisionTreeClassifier` and visualize it using `plot_tree`.

Make sure the feature matrix excludes both target columns. The resulting tree should show how the predictors distinguish the target combinations.

### 1(c) Convert the Decision Rules

Each path from the root to a leaf represents an IF-THEN rule.

You can traverse the fitted tree recursively, recording the feature and threshold at each split. Left branches correspond to values less than or equal to the threshold, while right branches correspond to values greater than it.

Use `export_text` to inspect the tree and verify that the extracted rules match its structure.

### 1(d) Cost-Complexity Pruning

Cost-complexity pruning controls tree complexity by penalizing additional terminal nodes.

Use `cost_complexity_pruning_path` to obtain candidate `ccp_alpha` values. For each candidate, fit a decision tree and evaluate its performance using cross-validation.

Compare the cross-validation accuracy and number of leaves for the candidate trees.

You can also consider the one-standard-error rule, which favors a simpler model when its performance is sufficiently close to the best cross-validation result.

If pruning does not improve validation performance, retaining the unpruned tree may be reasonable.

### 2(a) Obtain Data

Load `communities.data` with the supplied column names.

Use `na_values="?"` so missing entries are recognized as `NaN`.

Split the dataset according to the assignment's specified row positions rather than using a random train-test split.

Verify that the training and test sets contain the expected number of observations.

### 2(b) Missing Values

Remove columns that serve as identifiers rather than predictors.

For numerical predictors, use `SimpleImputer(strategy="mean")` to replace missing values.

Fit the imputer on the training data and transform the test data using the same fitted imputer. This prevents information from the test set from influencing preprocessing.

### 2(c) Correlation Matrix

Use `X_train.corr()` to calculate pairwise Pearson correlations between predictors.

A heatmap using `seaborn.heatmap` can help visualize the correlation structure.

Look for feature pairs with correlations close to +1 or -1, which indicate strong linear relationships.

### 2(d) Coefficient of Variation

The coefficient of variation measures relative variability:

CV = Standard Deviation / Mean

Calculate the mean and sample standard deviation of each predictor, then divide the standard deviation by the mean.

Be careful with features whose means are close to zero, since their coefficients of variation can become unusually large.

Sort the values to identify the predictors with the highest relative variability.

### 2(e) Scatter Plots and Box Plots

Select the requested number of predictors based on their coefficients of variation.

For each selected predictor, create a scatter plot against the response variable and a box plot showing its distribution.

Look for possible relationships, outliers, skewness, and differences in variability.

Remember that visual relationships do not establish statistical significance, and a weak individual relationship does not necessarily mean a predictor is unimportant in a multivariable model.

### 2(f) Linear Regression

Fit an ordinary least-squares model using `LinearRegression`.

Use the training set to estimate the coefficients and the test set to evaluate predictive performance.

Calculate the test MSE using `mean_squared_error` and record it for comparison with the regularized models.

### 2(g) Ridge Regression

Ridge regression adds an L2 penalty to the least-squares objective, shrinking coefficients toward zero.

Use `RidgeCV` or `GridSearchCV` to select the regularization parameter through cross-validation.

A logarithmically spaced grid is useful because suitable penalty values may vary across several orders of magnitude.

Evaluate the selected model on the test set and compare its MSE with ordinary least squares.

### 2(h) LASSO

LASSO uses an L1 penalty, which can shrink some coefficients exactly to zero and therefore perform feature selection.

Use `LassoCV` to choose the penalty parameter through cross-validation.

Consider fitting models with and without feature standardization. Since LASSO penalizes coefficient magnitudes, differences in feature scales can affect the selected variables.

For the standardized model, fit the scaler using only the training data.

After fitting, examine the nonzero coefficients and compare the selected features and test MSE between the two approaches.

For recent scikit-learn versions, use the supported `alphas` parameter rather than the deprecated `n_alphas` parameter.

### 2(i) Principal Components Regression

PCR first applies PCA to the predictors and then fits linear regression using the resulting principal components.

Since PCA is sensitive to feature scales, standardize the predictors before applying it.

A pipeline can combine `StandardScaler`, `PCA`, and `LinearRegression`.

Use `GridSearchCV` to determine the number of principal components that minimizes cross-validation error.

Then evaluate the selected model on the test set.

### 2(j) L1-Penalized Boosting Tree

XGBoost provides an L1 regularization parameter called `reg_alpha`.

You can use `XGBRegressor` with `GridSearchCV` to compare different penalty strengths.

To isolate the L1 penalty, set `reg_lambda=0`.

Try a range of values for `reg_alpha`, including zero, and select the value with the best cross-validation performance.

Evaluate the resulting model using test MSE and compare it against the earlier regression approaches.

Keep in mind that boosting also has other complexity-related parameters, such as tree depth, learning rate, and number of estimators.

### ISLR Conceptual Questions

For questions involving regularization, consider how the penalty parameter affects model flexibility.

With stronger regularization, coefficients are constrained more heavily, which generally increases bias and reduces variance.

As the constraint is relaxed, the model becomes more flexible. Training error generally decreases, while test error may follow a U-shaped trend because of the bias-variance tradeoff.

Variance tends to increase, squared bias tends to decrease, and irreducible error remains constant.

Use these relationships to evaluate the answer choices and justify your selections.

### Final Checks

Once you've run all the cells, verify that the notebook executes in order without errors, preprocessing is performed correctly, cross-validation is used for hyperparameter selection, and reported results match the notebook outputs.

Check that written interpretations are consistent with the results and that the installed library versions support the functions and parameters used.

### References

- [scikit-learn Decision Trees](https://scikit-learn.org/stable/modules/tree.html)
- [scikit-learn Cost-Complexity Pruning](https://scikit-learn.org/stable/auto_examples/tree/plot_cost_complexity_pruning.html)
- [scikit-learn SimpleImputer](https://scikit-learn.org/stable/modules/generated/sklearn.impute.SimpleImputer.html)
- [scikit-learn Linear Models](https://scikit-learn.org/stable/modules/linear_model.html)
- [scikit-learn PCA](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html)
- [scikit-learn GridSearchCV](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html)
- [XGBoost Parameters](https://xgboost.readthedocs.io/en/stable/parameter.html)
- [UCI Acute Inflammations](https://archive.ics.uci.edu/dataset/184/acute+inflammations)
- [UCI Communities and Crime](https://archive.ics.uci.edu/dataset/183/communities+and+crime)
