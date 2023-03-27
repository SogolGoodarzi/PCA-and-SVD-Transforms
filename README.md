# PCA-and-SVD-Transforms
## Introduction to PCA and SVD
***PCA***
Principal component analysis (PCA) is a popular technique for analyzing large datasets containing a high number of dimensions/features per observation, increasing the interpretability of data while preserving the maximum amount of information, and enabling the visualization of multidimensional data. Formally, PCA is a statistical technique for reducing the dimensionality of a dataset. This is accomplished by linearly transforming the data into a new coordinate system where (most of) the variation in the data can be described with fewer dimensions than the initial data. Many studies use the first two principal components in order to plot the data in two dimensions and to visually identify clusters of closely related data points. Principal component analysis has applications in many fields such as population genetics, microbiome studies, and atmospheric science.

![image](https://user-images.githubusercontent.com/125180530/227918507-eb66c85e-4383-4be7-af0f-6ea4371e5b02.png)

***SVD***
 Singular Value Decomposition (SVD) is a factorization of a real or complex matrix. It generalizes the eigendecomposition of a square normal matrix with an orthonormal eigenbasis to any m*n matrix. It is related to the polar decomposition. 
 
Specifically, the singular value decomposition of an m*n complex matrix M is a factorization of the form:

![image](https://user-images.githubusercontent.com/125180530/227918584-3d0902d2-8956-4ab0-b7a6-c30e2baa84ad.png)

where:

![image](https://user-images.githubusercontent.com/125180530/227918670-d647719f-33b8-4739-a304-e56a1bbdafcb.png)

Such decomposition always exists for any complex matrix. If M  is real, then U and V can be guaranteed to be real orthogonal matrices; in such contexts, the SVD is often denoted:

![image](https://user-images.githubusercontent.com/125180530/227918728-b56b77a8-96e9-4b35-a95d-34fcd9a97047.png)

In the figure below, you can see the functionality of this transform:

![image](https://user-images.githubusercontent.com/125180530/227918780-ed111dcd-887b-437d-b7ba-3e5b1f9a02bc.png)

## Implementing PCA
* Generate two sources that are random processes with uniform distributions. The first source (s1) has a uniform distribution in [-3,3] with T = 1000 samples and the second source (s2) has a uniform distribution in [-2,2] with T = 1000 samples as well. (Notice that it's better to change the mean of s1 and s2 to zero. For this aim you can subtract the mean of them from each value in these vectors).

Now consider the following matrix:

![image](https://user-images.githubusercontent.com/125180530/227918849-8911799d-f742-4b02-9bd9-5d6898487dfb.png)

With the use of the below formula, generate observation matrix X:

![image](https://user-images.githubusercontent.com/125180530/227918905-15def776-7941-43dc-a2f6-fe367b0ac9f8.png)

* The scatter plot of the observations is:

![image](https://user-images.githubusercontent.com/125180530/227919002-20844c3f-0169-4ae8-8fe5-fdf87f3227f1.png)

As you can see although the observations are three-dimensional, you can see they are scattered just in two dimensions. For a better understanding look at the following figure which is from another sight:

![image](https://user-images.githubusercontent.com/125180530/227919041-98c85dcb-105b-42e3-997d-a36ac852c382.png)

* In this step we have to calculate Rx which can be reached through the following formula:

![image](https://user-images.githubusercontent.com/125180530/227919083-b93fd2e7-e10d-493b-8fdb-ee5d8bd8ca90.png)

* For implementing PCA transform in MATLAB you can use 'eig' function. This function has two outputs including the D matrix corresponding to the eigenvalues matrix, and the U matrix corresponding to the eigenvectors matrix. The result of the implementation is as follows:

![image](https://user-images.githubusercontent.com/125180530/227919116-d9f07acb-36cc-4ce3-884c-2ca72b632500.png)

First of all, we sort the eigen values and corresponding eigen vectors:

![image](https://user-images.githubusercontent.com/125180530/227919153-714e384f-734d-4670-b063-162be65182e4.png)

***Conclusions***
1) As you can see one of the eigen values is zero. This means that the data doesn't have any projection in u3. In other words:

![image](https://user-images.githubusercontent.com/125180530/227914795-270f6fb8-eb77-4c68-a06e-4c5efad2fdfd.png)

2) u3 is orthogonal to the columns of matrix A because these are the columns that produced the data and in fact, the data is in the space of these columns. It means that:

![image](https://user-images.githubusercontent.com/125180530/227914843-14c54576-bf25-4167-91c3-27706d7d930d.png)

3) u1 and u2 are in the space of the columns of matrix A which are a1 and a2. It means that:

![image](https://user-images.githubusercontent.com/125180530/227914869-7ebe9079-7c64-4dd5-8d27-adff32150a07.png)

We can calculate matrix c:

![image](https://user-images.githubusercontent.com/125180530/227914928-3eda1b89-a2bd-4454-bdbe-d90c424c9607.png)

![image](https://user-images.githubusercontent.com/125180530/227914968-193b7266-18a5-41ca-9ba8-93530e7ceece.png)

We can also calculate it with MATLAB:

![image](https://user-images.githubusercontent.com/125180530/227915005-38fa0caa-db41-4042-9c29-d9e9b63b140d.png)

So we reach the same result:

![image](https://user-images.githubusercontent.com/125180530/227915045-edd88a56-807d-43f8-aac3-520fa31ee8c3.png)

* As it's said before, one of the eigenvalues is zero. So, the data has projections in just two dimensions. Therefore, we map the data in two dimensions with a transform matrix B:

![image](https://user-images.githubusercontent.com/125180530/227915105-a55d25ea-dcab-4a95-92d3-acfd2e4a4966.png)

We can call the B matrix the whitening matrix. It can be calculated as:

![image](https://user-images.githubusercontent.com/125180530/227915144-9fa44426-070a-45fb-a2e9-a1f0f38ec3a5.png)

![image](https://user-images.githubusercontent.com/125180530/227915173-8eb1896c-dbd4-4259-b286-ad2734743352.png)

Now we can show the scatter plot of the whitened data. You can see there are scattered just in two dimensions:

![image](https://user-images.githubusercontent.com/125180530/227915230-f0e42f22-b8b1-40b3-a2f9-1adc86104366.png)

We also plot the transformed data separately:

![image](https://user-images.githubusercontent.com/125180530/227915271-fe8f8517-6fa4-4328-8e82-c9d4ce253ca2.png)

One point to mention is that the whitened data should be uncorrelated and also the variance has to be 1. So, we can show that the process was valid because the variance is 1:

![image](https://user-images.githubusercontent.com/125180530/227915305-7ddd5851-05cd-4a69-a576-230df5d58eaf.png)

## Implementing SVD
* Now we want to implement SVD transform on observation matrix X like the following formula:

![image](https://user-images.githubusercontent.com/125180530/227915333-b896ad77-138c-45ad-8f9b-7d7d2cbf05a0.png)

We show the result of the implementation with matrices U and D that we reached before for better comparison:

![image](https://user-images.githubusercontent.com/125180530/227915372-7680524c-c427-420b-86c5-736e79f69ea6.png)

As you can see both of the matrices' values are the same. The difference is in the sign of values but it doesn't matter because we know that the columns of these matrices are vectors. If we change the sign of a vector, its size doesn't change. 

For the matrix of eigenvalues we have:

![image](https://user-images.githubusercontent.com/125180530/227915416-be8cc2cc-b535-499e-93bd-3c2452d34b0e.png)

![image](https://user-images.githubusercontent.com/125180530/227915456-cba15d0d-84e9-439c-ac8f-ac6c58242ef9.png)

As you can see the G matrix is the square root of the D matrix which is the matrix of eigenvalues. In other words, singular values are square roots of eigenvalues. 

Now we want to compare V^T with Z:

![image](https://user-images.githubusercontent.com/125180530/227915490-8b264d34-d8a8-4af1-a919-9f7cf014909d.png)

As you can see they have the same values. 

* In the previous parts, we saw that u1 and u2 were in the space of the columns of A which is a1 and a2. Now we want to show that the two first rows in V^T or z1(t) and z2(t) are in the space of the rows of matrix S. In other words:

![image](https://user-images.githubusercontent.com/125180530/227915525-b74c6dbd-e545-41e5-aba6-7ee97d68af60.png)

We can write:

![image](https://user-images.githubusercontent.com/125180530/227915560-9eebc4bd-7de7-47e5-a230-ecbd71ee4364.png)

![image](https://user-images.githubusercontent.com/125180530/227915592-1ed4a1e1-3d75-4f6a-9811-8a344ffa48cf.png)

So, we implement the process in MATLAB:

![image](https://user-images.githubusercontent.com/125180530/227915622-8b7ee6bc-1a9b-4417-ac3f-d499fec56103.png)

***Conclusion***
As it's obvious, the Z matrix is in the space of the sources matrix. So, we can conclude that source signals are orthogonal to the 3rd to Tth rows of V^T. So we can say:

![image](https://user-images.githubusercontent.com/125180530/227915674-09fd6210-676b-446f-a45b-fa64377380e9.png)

* The final question is how can we reduce the dimension of X such that 90% of the total energy of the observations remains?

The total energy of the observations can be calculated as follows:

![image](https://user-images.githubusercontent.com/125180530/227915705-8d0f7e50-8b24-44e7-a16f-5431a1487405.png)

![image](https://user-images.githubusercontent.com/125180530/227915743-bc918e82-3464-4a27-9bf6-8fd5cffb5099.png)

![image](https://user-images.githubusercontent.com/125180530/227915766-8cc5fb91-33a6-4ec5-ae37-3e596ab569d1.png)

Because we use just the first value of Landa and the inequality was valid for it, we can conclude that for reducing observations dimensions, we have to project them on the vector corresponding to this Landa. So we have:

![image](https://user-images.githubusercontent.com/125180530/227915794-661d2e96-5aef-47d6-8874-f09a5eabbdb0.png)

So, in this case, z3(t) shows the reduced observations. 

![image](https://user-images.githubusercontent.com/125180530/227915815-d37cb8c2-4413-4c73-9ccf-2a91477e035c.png)
