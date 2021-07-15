# Support Vector Machines (SVMs)

SVMs are a type of supervised learning algorithm that are used to classify data in a supervised fashion. SVMs are a very popular machine learning algorithm because of their ability to solve a wide variety of problems.

- It utilizes support vectors to define a decision boundary between groups.
- the support vector are the points that are closest to the decision boundary.
- The distance between the support vector and the decision boundary is called the margin.
- SVMs attempt to create the largest margin
- The c parameter controls how much error is allowed. Largest c value will allow less error (hard margin). Small c value will allow more error (soft margin). Small margin can result in overfitting. Large margin can result in underfitting.
- If the c value would be too big (overfitting), the SVMs will not be able to learn the data.
- SVMs uses kernels to classify points. A kernel can change how the data is separated. (e.g. linear, poly, rbf) Kernels can transform data into higher dimensions. A polynomial transforms the data into three dimensions, while rbf will transform data into infinite dimensions.
- An Radial basis function (rbf) kernel has a gamma parameter that controls how much the distance between points is affected. Large gamma can easily result in overfitting. Small gamma can result in underfitting.  

