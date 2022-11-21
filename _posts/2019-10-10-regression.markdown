---
layout: post
title: "ML Theory: Linear Models"
date: 2022-10-01 05:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: linear.jpg # Add image post (optional)
---
<strong>Regression:</strong> Regression is the task of estimating the value of one variable that's dependent on other variables. For example: determining the rent of a
house is a  function of the area of the house by square feet, the number of bedrooms, location and other facilities and the salary of a person is a function of his 
educational background and skill-set etc. There are lots of regression models. We will discuss only the linear model here. But the best in practice are Kernel Ridge 
regression, Support Vector regression, Lasso etc.   

<strong>Linear Regression</strong> Imagine that the features of a house can be numerically expressed as the following vector $x = (x_{1}, x_{2}, \cdots, x_{n})$ where $x_{1}$ can mean the number of kitchen or $x_{2}$ can mean whether there is a gym in the building or not. Our linear hypothesis is that if $y$ is the house rent, then,    
<center> $y = w_{1} x_{1} +  w_{2} x_{2} + \cdots +  w_{n} x_{n} + w_{n+1}$ </center>

So, if we extend the vector $x$ by one dimension by appending a dummy 1 at the end $x = (x_{1}, x_{2}, \cdots, x_{n}, 1)$, we can express $y$ as follows,   
<center> $y = w^{T}x$ </center>     
Where $w = (w_{1}, w_{2}, \cdots, w_{n}, w_{n+1})$    
So, if we are given $m$ data points $(x^{1}, y^{1}),(x^{2}, y^{2}),\cdots, (x^{m}, y^{m})$, the squared error for all data points should be:   
<center>$ E = \sum_{i=1}^{m} (y^{i} - w^{T}x^{i})^{2}$</center>



