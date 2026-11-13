### AI Use Log

#### Prompt:

I've attached my Homework 7 assignment PDF, my notebook template, and the Anuran Calls (MFCCs) data set and readme for context. Give me a brief, high-level outline of the relevant concepts, suggested methods, and what I should consider when interpreting my results. Don't provide complete solutions or write the notebook for me. I'll handle the implementation, testing, and written answers myself.


(Uploaded Homework7.pdf, bagai_sanchit_HW7.ipynb, Frogs_MFCCs.csv and Readme.txt for context)

#### Response:

I'll go through each section of Homework 7 and outline the relevant concepts, suggested methods, and considerations for interpreting the results without providing complete solutions or implementation code.

### 1(a) Obtain Data

Load the Anuran Calls (MFCCs) dataset and examine its features and three label columns: Family, Genus, and Species. Create the requested 70% training split and reserve the remaining data for testing.

### 1(b)(i) Multi-Label Evaluation Metrics

Research exact match accuracy, Hamming score, and Hamming loss. Understand how each metric evaluates predictions across multiple labels and what differences in their values indicate.

### 1(b)(ii) Gaussian Kernel SVM

Train separate classifiers for Family, Genus, and Species using the RBF kernel and one-versus-rest classification. Use 10-fold cross-validation to select the penalty parameter and kernel parameter. Consider how feature standardization affects the results.

### 1(b)(iii) L1-Penalized SVM

Repeat the classification using linear SVMs with L1 regularization. Standardize the features and use 10-fold cross-validation to select the penalty parameter. Consider how L1 regularization affects feature selection and model performance.

### 1(b)(iv) SMOTE

Investigate class imbalance in the three labels and apply SMOTE or another suitable method to address it. Ensure that oversampling is performed only on training data within each cross-validation fold. Compare the resulting performance with the previous classifiers.

### 2(a) K-Means Clustering

Apply K-Means to the complete dataset without a train-test split. Investigate methods such as silhouette scores, the Calinski-Harabasz index, gap statistics, or scree plots to select the number of clusters from 1 to 50.

Repeat the clustering procedure 50 times to examine variability across runs.

### 2(b) Majority Labels

For each cluster, identify the most frequent Family, Genus, and Species labels using the ground-truth data. Consider how cluster composition affects the assigned majority labels.

### 2(c) Hamming Metrics

Assign each observation the majority-label triplet of its cluster. Calculate the Hamming distance, Hamming score, and Hamming loss between the assigned labels and the true labels.

Summarize the results across the 50 repetitions, including the average and standard deviation of Hamming distances. Consider what these metrics reveal about clustering quality.

### Final Checks

Verify that preprocessing and cross-validation are performed correctly, confirm that the evaluation metrics are calculated consistently, and ensure that the written conclusions reflect the observed results. Compare the supervised classification methods and unsupervised clustering results while accounting for their different objectives.

### References

- [UCI Anuran Calls (MFCCs) Dataset](https://archive.ics.uci.edu/dataset/406/anuran+calls+mfccs)
- [NumPy Documentation](https://numpy.org/doc/stable/)
- [pandas Documentation](https://pandas.pydata.org/docs/)
- [Matplotlib Documentation](https://matplotlib.org/stable/)
- [scikit-learn Documentation](https://scikit-learn.org/stable/)
- [imbalanced-learn Documentation](https://imbalanced-learn.org/stable/)
- [SciPy Documentation](https://docs.scipy.org/doc/scipy/reference/)
- [Python collections Documentation](https://docs.python.org/3/library/collections.html)
