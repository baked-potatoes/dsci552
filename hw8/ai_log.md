### AI Use Log

#### Prompt:

I've attached my Homework 8 assignment PDF, my notebook template, and the data sets and readme for context. Give me a brief, high-level outline of the relevant concepts, suggested methods, and what I should consider when interpreting my results. Don't provide complete solutions or write the notebook for me. I'll handle the implementation, testing, and written answers myself.

(Uploaded Homework8.pdf, bagai_sanchit_HW8.ipynb, wdbc.data, wdbc.names, and data_banknote_authentication.txt for context)

#### Response:

I'll go through each section of Homework 8 and outline the relevant concepts, suggested methods, and considerations for interpreting the results without providing complete solutions or implementation code.

### 1(a) Obtain Data

Load the Breast Cancer Wisconsin (Diagnostic) dataset and examine its 30 features and binary diagnosis labels (Benign and Malignant). Identify the relevant feature and label columns and consider how the class distribution affects the subsequent experiments.

### 1(b) Monte Carlo Simulation

Repeat the supervised, semi-supervised, and unsupervised learning procedures 30 times using randomly selected training and test sets. Preserve the class proportions by selecting 20% of each class for testing.

Compare the average accuracy, precision, recall, F1-score, and AUC across the different methods. Consider how random splits affect the variability of the results.

### 1(b)(i) Supervised Learning

Train an L1-penalized linear SVM using normalized features. Use 5-fold cross-validation to select the penalty parameter.

Evaluate training and test performance across the 30 repetitions. Examine ROC curves and confusion matrices to understand classification performance and potential overfitting.

### 1(b)(ii) Semi-Supervised Learning

Randomly select 50% of each class in the training set as labeled data and treat the remaining observations as unlabeled.

Train an initial L1-penalized SVM using the labeled observations and cross-validation. Investigate self-training by iteratively assigning pseudo-labels to unlabeled observations farthest from the decision boundary.

Consider how confidence in pseudo-labels affects the final classifier and how errors introduced during self-training might propagate.

### 1(b)(iii) Unsupervised Learning with K-Means

Apply K-Means clustering to the training data with two clusters, ignoring the true labels during clustering.

Investigate random initialization and multiple restarts to reduce the likelihood of converging to a poor local minimum.

Assign class labels to clusters using majority voting among the 30 observations closest to each centroid. Evaluate training and test performance using the requested classification metrics.

Consider how distances to cluster centers can be used to construct scores for ROC analysis.

### 1(b)(iv) Spectral Clustering

Research spectral clustering and how it differs from centroid-based methods. Investigate the role of the RBF kernel and its gamma parameter in defining similarities between observations.

Repeat the clustering evaluation using two clusters and assign labels through majority voting within clusters.

Consider the limitations of assigning unseen test observations to clusters, since standard spectral clustering does not directly provide a prediction method for new data.

### 1(b)(v) Comparison of Learning Methods

Compare supervised, semi-supervised, K-Means, and spectral clustering results using their average classification metrics.

Consider the influence of labeled data availability, class distribution, and the assumptions made by each learning method. Examine whether the observed performance differences align with expectations.

### 2(a) Banknote Authentication Dataset

Load the Banknote Authentication dataset and examine its features and binary labels.

Randomly select 472 observations for testing and reserve the remaining 900 for training. Consider maintaining consistent experimental conditions when comparing active and passive learning.

### 2(b)(i) Passive Learning

Begin with 10 randomly selected training observations and train a linear L1-penalized SVM. Use 5-fold cross-validation to select the penalty parameter.

Incrementally add 10 randomly selected observations without replacement until all 900 training observations are used.

Repeat the procedure 50 times and record the test error at each training-set size. Consider how increasing the amount of labeled data influences generalization performance.

### 2(b)(ii) Active Learning

Begin with 10 randomly selected observations containing both classes and train a linear L1-penalized SVM.

At each iteration, select the 10 remaining observations closest to the decision boundary and add them to the training pool.

Repeat until all training observations are used, recording test errors at each step across 50 repetitions.

Consider why observations near the decision boundary may provide more useful information than randomly selected observations.

### 2(c) Learning Curves

Average the test errors across the 50 repetitions for each training-set size.

Plot the average test error against the number of training observations for both active and passive learning on the same figure.

Compare their convergence behavior, sample efficiency, and performance differences. Consider whether active learning provides an advantage when fewer labeled observations are available.

### Final Checks

Verify that normalization and cross-validation are performed correctly without introducing data leakage. Ensure that random sampling, class proportions, and evaluation metrics remain consistent across repetitions.

Confirm that the supervised, semi-supervised, and unsupervised comparisons reflect the observed results. For active and passive learning, ensure that training observations are selected without replacement and that the learning curves summarize all 50 repetitions.

### References

- [UCI Breast Cancer Wisconsin (Diagnostic) Dataset](https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic)
- [UCI Banknote Authentication Dataset](https://archive.ics.uci.edu/dataset/267/banknote+authentication)
- [NumPy Documentation](https://numpy.org/doc/stable/)
- [pandas Documentation](https://pandas.pydata.org/docs/)
- [Matplotlib Documentation](https://matplotlib.org/stable/)
- [scikit-learn Documentation](https://scikit-learn.org/stable/)
- [SciPy Documentation](https://docs.scipy.org/doc/scipy/reference/)
