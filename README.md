# Machine-Learning-APS-Failure-at-Scania-Trucks-Data-Set

The dataset consists of positive class (failure due to specific components of APS – Air Pressurized System) and negative class (failure due to other components not related to APS). The problem statement is to determine/minimize the total cost prediction model by correctly identifying the cases where the failure is due to APS.

The total cost prediction of a model is characterized by the sum of cost involved for unnecessary checks needed to be done by a mechanic and cost involved for missing a faulty truck, which may cause breakdown due to APS failure. The cost involved for missing a faulty truck due to APS failure is 500 while the cost involved for unnecessary check is 10. The best model should have less false negative and false positive predictions, in order to minimize the total cost of prediction model.

Datasets for training and testing have been down-sampled by factor of 3 (stratified), from the full-dataset versions with missing data on the UCI web site.
For more information on the dataset, and to access the full dataset:
https://archive.ics.uci.edu/ml/datasets/APS+Failure+at+Scania+Trucks

# Feature Engineering

The APS Failure at Scania Trucks data is associated with the classification task. There are in total 170 features with numeric attribute characteristics and 60,000 instances including missing values. Due to computation time, ‘smaller’ dataset with 19,999 training and 16,000 testing instances are considered for all the evaluations and analysis.

The attribute names of the data have been anonymized for proprietary reasons. It consists of both single numerical counters and histograms consisting of bins with different conditions. Typically the histograms have open-ended conditions at each end. For example if we measure the ambient temperature 'T' then the histogram could be defined with 4 bins where:

- bin 1 collect values for temperature T < -20
- bin 2 collect values for temperature T >= -20 and T < 0
- bin 3 collect values for temperature T >= 0 and T < 20
- bin 4 collect values for temperature T > 20

# Pre-processing
1. Data Parsing
2. Features with more than 75% missing instances are removed. 6 features are removed in total. 
2. Missing values in the feature set are compensated/filled using Mean imputed and Median imputed method (the number of missing values in original training set with 60000 training samples is 850015 and the number of missing values in smaller training set with 19999 training samples is 284543).
3. Compensate the unbalanced data set by adopting SMOTE (Synthetic Minority Oversampling Techniques) 
[Highly imbalanced dataset with 1000 positive class and 59000 negative class in 60000 training samples (Smaller training set with 333 positive class and 19666 negative class)].
4. Standardizing/ Normalizing the data

# Training and Classification 

- Total of 19999 training samples were considered for training (unbalanced data). Out of which 333 samples belongs to “pos” class and 19666 samples belongs to “neg” class.
- To oversample the minority class label “pos” samples, SMOTE is adopted by generating approximately 59 samples for every minority class training sample.
- Generated Balanced dataset contains 39322 training samples, out of which 19666 training sample belongs to each “pos” and “neg” class.
- Test data contains 16000 samples, out of which 375 sample belongs to “pos” label and 15625 sample belongs to “neg” label.
- Testing data with (or without) standardization using the corresponding training sample mean and standard deviation are used while testing data.
- Validation set is used in cross validation for choosing the best estimator (hypothesis) amongst different hyper parameters of a classifier (hypothesis set) and to avoid overfitting/underfitting.
- The model is trained on training set and tested on validation set, to choose the best hypothesis set based on the total cost incurred.
- The main objective is to minimize false positive and false negative samples/instances in order to minimize the total cost. Since the cost for false negative is high, recall must be higher in order to minimize the cost.
- ROC/ precision_recall curve is used to choose a threshold such that the recall is high and the total cost is minimized. Validation set is used for selecting threshold using cross validation.
- The best model test total cost obtained for Random Forest Classifier for training on balanced data set is 14060.
