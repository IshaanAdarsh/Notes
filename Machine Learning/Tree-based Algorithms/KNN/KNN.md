# [StatQuest: K-nearest neighbors](https://www.youtube.com/watch?v=HVXime0nQeI)
# [KNN Blog](https://towardsdatascience.com/k-nearest-neighbors-knn-explained-cbc31849a7e3)

# K-nearest neighbors (kNN):
![](https://miro.medium.com/v2/resize:fit:838/1*f5CmwipUB_I8BvDFwY26hg.png)

[Image source](https://questioneverything39.wordpress.com/2018/04/16/no-matter-what-group-you-join-its-all-group-think/)

K-nearest neighbors (kNN) is a supervised machine learning algorithm that can be used to solve both classification and regression tasks. I see kNN as an algorithm that comes from *real life*. People tend to be effected by the people around them. Our behaviour is guided by the friends we grew up with. Our parents also shape our personality in some ways. If you grow up with people who love sports, it is higly likely that you will end up loving sports. There are ofcourse exceptions. kNN works similarly.

> The value of a data point is determined by the data points around it.

-   If you have one very close friend and spend most of your time with him/her, you will end up sharing similarinterestsand enjoying same things. That is kNN with k=1.
-   If you always hang out with a group of *5, *each one in the group has an effect on your behavior and you will end up being the average of 5. That is kNN with *k=5*.

kNN classifier determines the class of a data point by majority voting principle. If k is set to 5, the classes of 5 closest points are checked. Prediction is done according to the majority class. Similarly, kNN regression takes the mean value of 5 closest points.

We observe people who are close but how data points are determined to be close? The distance between data points is measured. There are many methods to measure the distance. [Euclidean distance](https://en.wikipedia.org/wiki/Euclidean_distance) (minkowski distance with p=2) is one of most commonly used distance measurement. The figure below shows how to calculate euclidean distance between two points in a 2-dimensional space. It is calculated using the square of the difference between x and y coordinates of the points.

![](https://miro.medium.com/v2/resize:fit:1262/1*mFNKqdk8OEoRuZTD6Gnepw.png)

In the case above, euclidean distance is the square root of (16 + 9) which is 5. Euclidean distance in two dimensions remind us the famous [pythagorean theorem](https://en.wikipedia.org/wiki/Pythagorean_theorem).

It seems very simple for two points in 2-dimensional space. Each dimension represents a feauture in the dataset. We typically have many samples with many features. To be able to explain the concept clearly, I will go over an example in 2-dimensional space (i.e. 2 features).

> You can access all the code in this github [repo](https://github.com/SonerYldrm/kNN_Algorithm). Feel free to use it!

Let's start with importing libraries:

![](https://miro.medium.com/v2/resize:fit:1204/1*5UJ8J6Wjr5p022KFs5SnRw.png)

> Scikit-learn provides many useful functions to create synthetic datasets which are very helpful for practicing machine learning algorithms. I will use **make_blobs** function.

![](https://miro.medium.com/v2/resize:fit:1070/1*x9TXSH2pvTgkKkGYsXDCdw.png)

This code creates a dataset with 100 samples divided into 4 classes and the number of features is 2. Number of samples, features and classes can easily be adjusted using related parameters. We can also adjust how much each cluster (or class) is spread. Let's visualize this synthetic data set:

![](https://miro.medium.com/v2/resize:fit:1278/1*mIZIT4gU00epZDGczf5csw.png)

For any supervised machine learning algorithm, it is very important to divide dataset into train and test sets. We first train the model and test it using different parts of dataset. If this separation is not done, we basically test the model with some data it already knows. We can easily do this separation using **train_test_split** function.

![](https://miro.medium.com/v2/resize:fit:1256/1*FdaWpR7lVALxwVYY6D-i0w.png)

We can specify how much of the original data is used for train or test sets using **train_size** or **test_size** parameters, respectively. Default separation is 75% for train set and 25% for test set.

Then we create a kNN classifier object. To show the difference between the importance of k value, I create two classifiers with k values 1 and 5. Then these models are trained using train set. **n_neighbors** parameter is used to select k value. Default value is 5 so it does not have to be explicitly written.

![](https://miro.medium.com/v2/resize:fit:814/1*liV2Z3nVikWSLwUzjDXfTg.png)

Then we predict the target values in the test set and compare with actual values.

![](https://miro.medium.com/v2/resize:fit:544/1*yqCc4NTu8cIBV650tyIxkg.png)

In order to see the effect of k values, let's visualize test set and predicted values with k=5 and k=1.

![](https://miro.medium.com/v2/resize:fit:1220/1*atqT9EydQN3YGTxtCLU-RA.png)

![](https://miro.medium.com/v2/resize:fit:1220/1*0fhvGdmPoECczxRGFW7Vlg.png)

![](https://miro.medium.com/v2/resize:fit:1220/1*kYtAkcvW1GoOa8Eieqm2Ow.png)

The result seems to be very similar because we used a substantially small dataset. However, even on small datasets, different k values predict some points differently.

How to find the best k value
============================

-   **k=1**: The model is too specific and not generalized well. It also tends to be sensitive to noise. The model accomplishes a high accuracy on train set but will be a poor predictor on new, previously unseen data points. Therefore, we are likely to end up with an overfit model.
-   **k=100**: The model is too generalized and not a good predictor on both train and test sets. This situation is known as underfitting.

How do we find the optimum k value? Scikit-learn provides **GridSearchCV **function that allows us to easily check multiple values for k. Let's go over an example using a dataset available under scikit-learn datasets module.

![](https://miro.medium.com/v2/resize:fit:1026/1*6DXcH7ypnMZmNXF6uGZhWQ.png)

After we import the required libraries and load the dataset, we can create a GridSearchCV object.

![](https://miro.medium.com/v2/resize:fit:1230/1*MflibQv6WVklZtwF6UTcHg.png)

We do not need to split the the datasets because **cv** parameter splits the dataset. The default value for cv parameter is 5 but I explicitly wrote it to emphasize why we don't need to use train_test_split.

cv=5 basically splits the dataset into 5 subsets. GridSearchCV does 5 iterations and use 4 subsets for training and 1 subset for testing at each time. In this way, we are able to use all data points for both training and testing.

We can check which parameters give us best results using **best_params_ **method:

![](https://miro.medium.com/v2/resize:fit:398/1*xoH9lp6f1HzCuMETwy6ygA.png)

In this case, the optimum value for k is 12.

Pros and cons of k-Nearest-Neigbors
===================================

**Pros**

-   Simple and easy to interpret
-   Does not make any assumption so it can be implemented in non-linear tasks.
-   Works well on classification with multiple classes
-   Works on both classification and regression tasks

**Cons**

-   Becomes very slow as the number of data points increases because the model needs to store all data points.
-   Not memory efficient
-   Sensitive to outliers. Outliers also have a vote!
