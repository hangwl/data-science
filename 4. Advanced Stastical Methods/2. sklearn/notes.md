# About sklearn

Scikit-learn (sklearn) is a ML tookit in Python

pandas dataframes useful for statsmodel

numpy's ndarrays necessary for sklearn

Advantages:
    Good documentation <https://scikit-learn.org/stable/>
    Large variety of ML techniques
    Deep-learning can supplemented by TensorFlow, Keras, PyTorch as alternatives
    Numerically stable - if numbers are too small or too big, errors could occur

# Machine Learning
3 types - supervised, unsupervised, reinforcement
    Supervised - Inputs(features to predict targets) and Targets(outcomes)

Standardization (Feature Scaling)- process of subtracting the mean and dividing by the standard deviation (transforming data into standard scale - mean of 0 and sd. of 1)
    Easy fix to the most common problem in working with numerical data caused by difference in magnitudes
    AKA feature scaling or normalization (which may refer to other concepts in ML)
        Having all inputs with the same magnitude allows us to compare their impact

Normalization - has different meaning depending on the case
    in sklearn reg.fit(), subtract the mean but divide by the L2-norm of the inputs
        Take note of other default parameters:
            copy_X=True
            fit-intercept=True
            n_jobs=1
            normalize=False
    See Wiki article on Feature scaling <https://en.wikipedia.org/wiki/Feature_scaling>
    See article on L1-norm and L2-norm <http://www.chioka.in/differences-between-the-l1-norm-and-the-l2-norm-least-absolute-deviations-and-least-squares/>

Feature selection simplifies models by removing unnecessary features
    feature_selection.f_regression
        F-regression creates simple linear regressions of each feature and the dependent variable

Underfitting and Overfitting
    - an underfitted model has low train accuracy, low test accuracy
    - overfitted model has high train accuracy, but captures all the noise, and thus has low test accuracy
    - a good model should have high accuracy in both train and test data
      - it makes sense to split data into 2 parts, training and testing
        - train model on training dataset and test it on testing dataset