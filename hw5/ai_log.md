### AI Use Log:

#### Prompt:

I've attached my Homework 5 assignment PDF and my notebook template for context. Can you help me work through the problems and the ISLR questions? For each part, explain the steps and include the relevant Python code with suggested variable names, plus the written answers, so I can run and test everything myself on the data.
(Uploaded Homework4.pdf and bagai_sanchit_HW4.ipynb for context)

#### Response:

## Response:

### Imports

Provided a single import cell for the whole assignment (numpy, pandas, matplotlib, seaborn, scikit-learn tree/linear/decomposition/model-selection tools, and xgboost), with comments removed at my request.

### 1(a) Obtain Data

Load `diagnosis.data` (UTF-16, tab-separated, decimal comma) with `pd.read_csv`, name the 8 columns, and map yes/no to 1/0.

```python
df = pd.read_csv(path, sep="\t", header=None, names=cols, encoding="utf-16", decimal=",")
df = df.replace({"yes": 1, "no": 0})
```

### 1(b) Build a Decision Tree

The data set is multi-label, so I used the label powerset method: the two labels are combined into one four-class label, and a single `DecisionTreeClassifier` is fit on the whole data set and plotted with `plot_tree`.

```python
y = df["bladder_inflammation"].astype(str) + "_" + df["nephritis"].astype(str)
clf = DecisionTreeClassifier(random_state=42).fit(X, y)
```

### 1(c) Convert the Decision Rules

A recursive `tree_to_rules` function walks the fitted tree and turns each root-to-leaf path into an IF-THEN rule. `export_text` prints the same tree as text.

### 1(d) Cost-Complexity Pruning

Used `cost_complexity_pruning_path` and 5-fold cross-validation over the candidate `ccp_alpha` values. The first version chose the largest tied alpha, and the one-standard-error rule was tried next. Both chose `ccp_alpha = 0.0`.

A table of alpha, leaf count and CV accuracy showed why. The unpruned tree has 6 leaves and CV accuracy 0.992, and pruning to 4 leaves drops it to 0.883. The unpruned tree is therefore already minimal.

### 2(a) Obtain Data

Load `communities.data` with the 128 column names and `na_values="?"`, then split by position: the first 1495 rows are the training set and the remaining rows are the test set.

### 2(b) Missing Values

Dropped the five nonpredictive columns (`state`, `county`, `community`, `communityname`, `fold`) and applied `SimpleImputer(strategy="mean")`, fit on the training set only and applied to the test set.

### 2(c) Correlation Matrix

`seaborn.heatmap` of `X_train.corr()`, plus a list of the most strongly correlated feature pairs.

### 2(d) Coefficient of Variation

CV = sample standard deviation / mean (`ddof=1`) per feature, sorted by absolute value.

### 2(e) Scatter Plots and Box Plots

Selected the floor(sqrt(128)) = 11 features with the highest CV and made scatter plots against the target and box plots.

Scatter plots alone cannot establish significance, because the features are skewed with no clear trend and visual patterns cannot account for interactions with other features.

### 2(f) Linear Model

`LinearRegression` on the training set. Test MSE 0.01814.

### 2(g) Ridge Regression

`RidgeCV` with a log-spaced alpha grid and 10-fold CV. Best lambda about 3.51, test MSE 0.01754.

### 2(h) LASSO

`LassoCV` with 10-fold CV, once on the raw features and once on standardized features (scaler fit on the training set). `n_alphas` was removed because the installed scikit-learn version no longer accepts it.

The raw fit has test MSE 0.01774 with 75 of 122 variables selected. The standardized fit has test MSE 0.01784 with 76 variables selected. 71 variables are selected in both.

### 2(i) PCR

A `Pipeline` of `StandardScaler`, `PCA` and `LinearRegression`, with the number of components M tuned by `GridSearchCV` (10-fold CV). Best M = 96, test MSE 0.01843.

### 2(j) L1-Penalized Boosting Tree

`XGBRegressor` with `reg_alpha` (the L1 penalty) tuned by `GridSearchCV` over [0, 0.001, 0.01, 0.1, 1, 10, 100], with `reg_lambda=0` so that L1 is the only penalty. Best alpha 0.1, test MSE 0.01615, the lowest of all models.

### Final Checks

Checked the notebook for errors, execution order and leftover typos, and suggested pinned library versions for the environment file.

### References:

- scikit-learn DecisionTreeClassifier: https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html
- scikit-learn cost-complexity pruning: https://scikit-learn.org/stable/auto_examples/tree/plot_cost_complexity_pruning.html
- scikit-learn export_text: https://scikit-learn.org/stable/modules/generated/sklearn.tree.export_text.html
- scikit-learn SimpleImputer: https://scikit-learn.org/stable/modules/generated/sklearn.impute.SimpleImputer.html
- scikit-learn LinearRegression: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html
- scikit-learn RidgeCV: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.RidgeCV.html
- scikit-learn LassoCV: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LassoCV.html
- scikit-learn PCA: https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html
- scikit-learn GridSearchCV: https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html
- XGBoost parameters: https://xgboost.readthedocs.io/en/stable/parameter.html
- UCI Acute Inflammations: https://archive.ics.uci.edu/ml/datasets/Acute+Inflammations
- UCI Communities and Crime: https://archive.ics.uci.edu/ml/datasets/Communities+and+Crime
