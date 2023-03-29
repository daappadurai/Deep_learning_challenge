# **Deep Learning challenge**

## **Overview:**

The goal of this analysis is to design a deep learning neural network model that will assist Alphabet Soup Charity organization to determine whether or not an applicant organization will receive funding based several criteria such as application type, affiliation, use case, ask amount to name a few. The full list of criteria is listed below:

EIN <br>
NAME OF THE ORGANIZATION <br>
APPLICATION TYPE <br>
AFFILIATION <br>
CLASSIFICATION <br>
USE CASE <br>
ORGANIZATION <br>
STATUS <br>
INCOME AMT <br>
SPECIAL CONSIDERATIONS <br>
ASK AMT <br>
IS SUCCESSFUL <br>

## **Data preprocessing:**

Deep learning neural networks only take in numerical values as input. Therefore, all categorical variables should be numerically encoded before feeding the data into the model. The categorical variables are first checked for unique values. If the number of unique values is less than 10 then they are ready for encoding. If unique values within a categorical variable is greater than 10 then those categories within the categorical variable which are smaller in number are all grouped together. The rationale is that these rare categories do not significantly contribute to the overall selection process. The kernel density plot will help establish a cutoff range for the insignificant categories within a categorical variable. After binning the less significant categories within a categorical variable, all the categorical variables first are taken out into a separate dataframe so that they can all be processed at the same time using one hot encoder which assigns numerical values for each entry within a categorical variable. Once these categorical variables are encoded, they are merged back to the original dataframe. After merging, the initial unencoded categorical variables are dropped.

The target variable is IS_SUCCESSFUL which tells whether an application organization is received funding.
The main features are as follows:

APPLICATION TYPE (one-hot encoded)<br>
AFFILIATION (one-hot encoded)<br>
CLASSIFICATION (one-hot encoded)<br>
USE CASE (one-hot encoded)<br>
ORGANIZATION (one-hot encoded)<br>
STATUS (one-hot encoded)<br>
INCOME AMT (one-hot encoded)<br>
SPECIAL CONSIDERATIONS (one-hot encoded)<br>
ASK AMT 

The identification number (EIN) and the Name of the organization are neither targets or features and should be removed from the input data.

## **Neural network parameters:**

The TensorFlow and keras dependencies are utilized to create the neural network. The neural network model has one input layer, one hidden layer and one output layer with the following parameters:
1.	Number of input features = number of independent variables
2.	The number of neurons in input layer = 8
3.	The number of neurons in hidden layer = 5

The activation function for the first layer and the hidden layer is relu while the output layer uses the sigmoid function. The model is run for a 100 epochs.

## **Model performance evaluation:**

Model performance is tracked by the level accuracy reached by the end of 100 epochs. The model is run three times with the following adjustments.

Attempt 1 – Number of neurons in the output layer = 8; (accuracy, train: 0.7361, test: 0.7237)
                      Number of neurons in the hidden layer = 5

Attempt 2 – Number of neurons in the output layer = 15; (accuracy, train: 0.7372, test: 0.7267)
                      Number of neurons in the hidden layer = 5

Attempt 3 - Number of neurons in the output layer = 8; (accuracy, train: 0.7360, test: 0.7264)
                      Number of neurons in the hidden layer 1 = 5
	         Number of neurons in the hidden layer 2 = 5
		



## **Model Optimization using Keras tuner:**

The Keras turner was utilized to determine the activation function, (relu, tanh, sigmoid) that is appropriate for the input and the hidden layer with neurons ranging from 1-10. The output layer has one neuron with a sigmoid activation function. The model is run for 20 epochs.
This did not significantly improve the accuracy which was 0.7276 for both testing and training.



## **Possible explanation for lack of improvement in accuracy:**

Even after making several attempts to improve the efficiency, there was not a significant improvement in accuracy. The model is statistically and mathematically sound. The data should be the limiting factor. When closely analyzing the data, the funding amount (ASK_AMT) is not thoroughly investigated. Upon checking the funding amounts it became obvious that the data is extremely skewed, with over 25,000 grants that were $5000 and the rest of the grant amounts are 3 or less. Moreover, the maximum funding amount is 8.597801e+09. Extremely skewed or non-normal data violates scaling requirement, which assumes the data is normally distributed. Therefore, this skewed column could be the reason why the accuracy cannot be improved.

## **Recommendation for improving the model:**

1.	Outlier test: As a first step, an outlier test should be performed to remove extreme outliers. 
2.	Categorize the grant funding (ASK_AMT) variable. The ask amount should be converted to a string and categorized. 
3.	Numerical encoding:  The ASK_AMT variable should be numerically encoded with one hot encoder and scaled. 
4.	Finally rerun the model with keras tuner, document train and test accuracy and losses.













