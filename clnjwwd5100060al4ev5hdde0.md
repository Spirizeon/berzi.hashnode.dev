---
title: "Deep Learning: Regression feat. Linear algebra"
datePublished: Tue Oct 10 2023 05:59:14 GMT+0000 (Coordinated Universal Time)
cuid: clnjwwd5100060al4ev5hdde0
slug: dlrfla

---

## What is Linear Regression?

In simple words, Linear regression is a type of machine learning model training method that helps it predict data after being trained from existing data points.

We aim to build a linear equation from existing data points,

$$y_i = \beta_1x_i + \beta_0$$

But we don't know the parameters:

$$\beta_1 , \beta_0$$

We first calculate the errors between our assumed equation with randomized parameters and the existing y-values from the data points, we term them as residuals.

$$\epsilon = \beta_1 x + \beta_0 -y_i$$

Then we average the errors. (We call this the cost function)

$$U = \frac{1}{n} \sum_{i=1}^{n} \epsilon^2$$

If we consider only the sum of squares of residuals, we call that the Loss function.

Although the expression looks weird, we arrive at a weirder question...

### Why MSE and not RMSE??

MSE (mean square error) will let us differentiate the expression better.

#### Case of RMSE

$$U = \sqrt{ \sum_{i=1}^{n} \epsilon^2}$$

Then differentiation of RMSE would become

$$\nabla U =\frac{1}{2} \sum_{i=1}^{n} \biggl[ \begin{array}{cc} \frac{1}{|\epsilon|} \\ \frac{\beta_1}{|\epsilon|} \end{array} \biggr]$$

Now since the residual is smaller than 1 (in some cases), the gradient is very big, hence it is a non-conventional way of doing things.

#### Going back to the point

Here's what should be done.

We will partially differentiate the MSE equation concerning the parameters that we wish to find out

$$\nabla U = \sum^n_{i=1}\biggl[ \begin{array}{c}2(\beta_1 x_i + \beta_0 - y_i) \\ 2 \beta_1 (\beta_1 x_i + \beta_0 - y_i) \end{array} \biggr]$$

Then we calculate the step size

$$\text{Step-size} = \text{Learning-rate} (\eta) \times (-\text{slope}) (\nabla U)$$

Step size is the distance between two consecutive residuals, the slope is their respective derivative, we introduce another variable called learning rate and randomize it at first (but keep it small)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1696917313588/027204ec-1af9-410f-bdf7-3b7f668d15c4.webp align="center")

We calculate the new intercept until the concerned component of derivatives tends to 0. We repeat this process for every parameter and finally finalize a linear equation.

$$\text{New-intercept} = \text{Step-size} + \text{Old-intercept}$$

### References, Sources and material

* https://github.com/spirizeon/linear\_regression
    
* Oreilly Deep Learning: A practitioner's approach
    
* [https://github.com/DotSlash-A/BSCS3004-Deep-Learning-resources](https://github.com/DotSlash-A/BSCS3004-Deep-Learning-resources)