# One-Sample z-test - Lab

## Introduction
In this lab, you'll perform a few quick tests to help you better understand how hypothesis testing works.

## Objectives
You will be able to:

* Explain use cases for a 1-sample z-test
* Set up null and alternative hypotheses
* Use the z-table and scipy methods to acquire the p value for a given z-score
* Calculate and interpret p-value for significance of results

## Exercise 1
A fast-food chain claims that the mean time to order food at their restaurants is 60 seconds, with a standard deviation of 30 seconds. You decide to put this claim to the test and go to one of the restaurants to observe actual waiting times. You take a sample of 36 customers and find that the mean order time was 75 seconds. Does this finding provide enough evidence to contradict the fast food chain's claim of fast service?

Follow the 5 steps shown in previous lesson and use $\alpha$ = 0.05. 


```python
# Importing the required modules
import scipy.stats as stats
from math import sqrt
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
```


```python
# State your null and alternative hypotheses
alternative_hypothesis = "The Sample Mean for the customer's wait time in a fast-food chain restaurant is Significantly bigger than the Population mean."
null_hypothesis = "There is no Significance difference between the Sample Mean and the Population Mean of a fast-food chain restaurant's wait time."
```


```python
"""
We need to calculate the z-statistics using the formula: z = (x_bar - mu)/(sigma/sqrt(n)). 
Variables will first be declared and applied in the mentioned formula.
"""
# sample mean
x_bar = 75

# Number of customers sampled
n = 36

# Standard Deviation of the population
sigma = 30

# Population mean
mu = 60

# Z-Statistics for z-test
z = (x_bar - mu)/(sigma/sqrt(n))
f'z-test value: {z}'
# (p = 0.0013498980316301035, z = 3.0)
```




    'z-test value: 3.0'




```python
# Set the tableau-colorblind10 style
plt.style.use('tableau-colorblind10')

# Calculate the x and y values for the standard normal distribution
x = np.linspace(-4, 4, 1000)
y = stats.norm.pdf(x)

# Create the plot
# plt.plot(x, y, label='Standard Normal Distribution')

# Plot the vertical line at z=3.0
plt.axvline(x=3.0, color='blue', alpha=0.5, linestyle=':', label='z-test value = 3.0')

# Shade the area below z=3.0
plt.fill_between(x, y, where=(x <= 3.0), color='red', alpha=0.35, label='Area Below z-statistics')

# Shade the area above z=3.0
plt.fill_between(x, y, where=(x >= 3.0), color='blue', alpha=0.35, label='Area Above z-statistics')

# Add labels and title
plt.xlabel('z-value')
plt.ylabel('Probability Density')
plt.title('Standard Normal Distribution: z-statistics = 3.0')

# Add legend positioned in the top-left corner
plt.legend(loc='upper right', fontsize='small', frameon=True)

plt.xticks(fontsize=7)
plt.yticks(fontsize=7)

# Reduce the transparency of the outer black lining
plt.gca().spines['left'].set_alpha(0.35)
plt.gca().spines['bottom'].set_alpha(0.35)
plt.gca().spines['right'].set_alpha(0.35)
plt.gca().spines['top'].set_alpha(0.35)

# Add dotted grid lines
plt.grid(linestyle='dotted')

# Show the plot
plt.show()
```


    
![png](output_4_0.png)
    



```python
"""Calculating the p-value"""
# Calculating the cumulative probability
cum_prob = stats.norm.cdf(z)

# Getting the p-value
p = 1 - cum_prob
f'p-value: {p}'
```




    'p-value: 0.0013498980316301035'




```python
# Explaining the results above
"""
The p-value (0.0013498980316301035) is less than the significance level (0.05) and therefore, we reject the null hypotheis.
The Sample Mean for the customer's wait time in a fast-food chain restaurant is Significantly bigger than the Population mean.
There is evidence to say that it takes more time to order in this fast food-chain restaurant.
"""
```




    "\nThe p-value (0.0013498980316301035) is less than the significance level (0.05) and therefore, we reject the null hypotheis.\nThe Sample Mean for the customer's wait time in a fast-food chain restaurant is Significantly bigger than the Population mean.\nThere is evidence to say that it takes more time to order in this fast food-chain restaurant.\n"



## Exercise 2

25 students complete a preparation program for taking the SAT test.  Here are the SAT scores from the 25 students who completed the program:

``
434 694 457 534 720 400 484 478 610 641 425 636 454 
514 563 370 499 640 501 625 612 471 598 509 531
``

We know that the population average for SAT scores is 500 with a standard deviation of 100.

Are our 25 students’ SAT scores significantly higher than the population's mean score? 

*Note that the SAT preparation program claims that it will increase (and not decrease) the SAT score.  So, you can conduct a one-directional test. (alpha = .05).*


```python
# Stating the hypotheses below

# Alternative hypothesis (Ha: mu < xbar)
alternative_hypothesis = "The sample mean of SAT scores for 25 students is siginificantly higher than the population's mean score."

# Null hypothesis (H0: mu >= xbar)
null_hypothesis = "There is no significant difference between the sample mean and the population mean."
```


```python
# Calculating the z-statistics using the formula: z = (x_bar - mu)/(sigma/sqrt(n)). 

# sample mean
x_bar = sum(set([434, 694, 457, 534, 720, 400, 484, 478, 610, 641, 425, 636, 454, 514, 563, 370, 499, 640, 501, 625, 612, 471, 598, 509, 531]))/25

# Number of students who sat for SAT test
n = 25

# Standard Deviation of the population
sigma = 100

# Population mean
mu = 500

# Z-Statistics for z-test
z = (x_bar - mu)/(sigma/sqrt(n))
f'z-test value: {z}'

# z = 1.8
```




    'z-test value: 1.8'




```python
# Set the tableau-colorblind10 style
plt.style.use('tableau-colorblind10')

# Calculate the x and y values for the standard normal distribution
x = np.linspace(-4, 4, 1000)
y = stats.norm.pdf(x)

# Create the plot
# plt.plot(x, y, label='Standard Normal Distribution')

# Plot the vertical line at z=1.8
plt.axvline(x=1.8, color='blue', alpha=0.5, linestyle=':', label='z-test value = 1.8')

# Shade the area below z=1.8
plt.fill_between(x, y, where=(x <= 1.8), color='red', alpha=0.35, label='Area Below z-statistics')

# Shade the area above z=1.8
plt.fill_between(x, y, where=(x >= 1.8), color='blue', alpha=0.35, label='Area Above z-statistics')

# Add labels and title
plt.xlabel('z-value')
plt.ylabel('Probability Density')
plt.title('Standard Normal Distribution: z-statistics = 1.8')

# Add legend positioned in the top-left corner
plt.legend(loc='upper right', fontsize='small', frameon=True)

plt.xticks(fontsize=7)
plt.yticks(fontsize=7)

# Reduce the transparency of the outer black lining
plt.gca().spines['left'].set_alpha(0.35)
plt.gca().spines['bottom'].set_alpha(0.35)
plt.gca().spines['right'].set_alpha(0.35)
plt.gca().spines['top'].set_alpha(0.35)

# Add dotted grid lines
plt.grid(linestyle='dotted')

# Show the plot
plt.show()
```


    
![png](output_10_0.png)
    



```python
"""Calculating the p-value"""
# Calculating the cumulative probability
cum_prob = stats.norm.cdf(z)

# Getting the p-value
p = 1 - cum_prob
f'p-value: {p}'
# p = 0.03593031911292577, 
```




    'p-value: 0.03593031911292577'




```python
# Interpret the results in terms of the p-value
"""
With a our p-value (0.03593031911292577) being less than the stated significance level (0.05),'
we reject the Null Hypothesis. The SAT scores for the 25 students are significantly higher than the population mean score.
There is evidence to say that the SAT preparation program is helping the students increase their SAT scores.
"""
```




    "\nWith a our p-value (0.03593031911292577) being less than the stated significance level (0.05),'\nwe reject the Null Hypothesis. The SAT scores for the 25 students are significantly higher than the population mean score.\nThere is evidence to say that the SAT preparation program is helping the students increase their SAT scores.\n"



## Summary

In this lesson, you conducted a couple of simple tests comparing sample and population means, in an attempt to reject our null hypotheses. This provides you with a strong foundation to move ahead with more advanced tests and approaches later on.
