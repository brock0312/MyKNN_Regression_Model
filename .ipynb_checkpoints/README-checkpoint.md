# MyKNN_Regression_Model
### *Abstract*
 K-nearest-neighbors (KNN) is a power method to construct nonparametric regression models. To better understand how the model works, I tried to  construct a KNN regressor without using specialized data structures such as the K-D tree to speed up the process. That is, I'm going to apply the "brute-force" method to find nearest neighbors.
 
 Given a set of 𝑁 training data points and a pre-defined hyper-parameter, k, the prediction for a testing data point X𝑎 is computed by locating  𝑘 data points in the training data that is cloest to X𝑎. If the outcome values of the 𝑘 nearest neighbors are  𝐲𝑎={𝑦1,𝑦2,...,𝑦𝑘}, then the   prediction is 𝑓(𝐲𝑎), where 𝑓 is a real-valued function. 
 
 Here I'm going to consider two possible choices of 𝑓. 
 
 The first option is 𝑓(𝐲𝑎)=1/𝑘∑𝑘𝑖=1𝑦𝑖. This is referred to as the "equal-weight" case. 
 The other option is to compute the mean after removing outliers. We define outliers as the data points that are outside of  [𝑄1−1.5𝐼𝑄𝑅,𝑄3+1.5𝐼𝑄𝑅], where 𝑄1 and 𝑄3 are the first and third quantile of 𝐲𝑎, and 𝐼𝑄𝑅=𝑄3−𝑄1.
 
 Since quantiles and IQR only make sense when there are enough neighbors, I'm going to set a parameter that allows the "remove_outliers" only if 𝑘 >= 10. If 𝑘 < 10, I'll use the "equal_weight" 𝑓 even if the user specify the other way.
 
###  *Dataset*
 I'm going to use a subset of the "Million Songs Dataset" to test the regressor. The dataset, msd_data1.pickle, has been pre-processed and the training and testing dataset has been splitted and stored in a dictionary data structure. There are four elements in the dictionary: x_train, y_train, x_test, y_test. As indicated by their names, these four elements are training and testing data. The outcome variable is the year a song was released, and the features are variables that characterize the sound of a song. The goal is to predict the release year given sound features.

###  *Prediction Outcomes*
 I'm going to standardize all feature values and make predictions using 𝑘=20 with both "equal_weight" and "remove_outier" to see the differences. Also I'll list out the RMSE(Root Mean Squared Error) to evaluate the performance of the regressor, and show the first 20 predictions in the testing data.
 
###  *Parameter Tuning*
  I'm going to further explore the issue of hyper-parameter tuning by considering three cases using the knn regressor from klearn.neighbors.KNeighborsRegressor for the first two cases, and my own myknn_regressor for the third cases.

  For each case, I'll use the data from msd_data1.pickle to train and test the KNN models, then compute the RMSE values on the testing dataset using 𝑘=1,2,3,4,5,10,15,20,25,30,35,40,45,50,55,60,80,100,120,140,160,180,200 to figure out the optimal k in each case. To differenciate the first two cases, I'll standardize all feature value in case 1 and won't apply any feature scaling in case 2. As for case 3, I'll use standardized feature and adopted myknn_regressor with "remove_outlier" to make prediction.

