---
Title: "What statitical tests are essential to learn for a biologist"
Date: 2025-06-23
Author: MA Anwar
---
There are hundereds of statistical tests that have been proposed over the years for various situations. However, it is not feasible to master all these tests even for statistician, let alone a biologist should learn these. Here, lets dive into the most prominent tests that are frequently used by biologists and should be learnt for effective research. 

### **Comparing group differences**
### 1. t-test
  The most basic stattistical test used to compare the means of two samples or one sample (one value to a sample). It assumes normality meaning that the data should be normaly distributed and their variances should be equal. Normal distribution is difficult to achieve in real-world situations, therefore, an alternative    to standard t-test, **Welch's t-test** sould be used (aka unequal variances t-test). Welch's t-test does not assume normality of data, and can work with unequal number of data points in each sample. In **R**, the default t-test performs Welch's t-test, however, in **python** (scipy), one needs to specify equal_var=False
```{r}
t_test <- t.test(a, b,
                 alternative = c("two.sided"),
                 paired = False, # whether the study subjects are same before and after teh exp.
                 var.equal = F)
```


```{python}
from scipy.stats import ttest_ind
t_test = ttest_ind(a, b,
                   equal_var=False,
                   axis=0) # Welch's t-test 
```


#### 3. Mann-Whitney U test
  Non-parametric test to evaluate the stochastic superioirty of one distribution over the other. 

#### 4. Wilcoxon signed-rank test
  Wilcoxon signedrank test is also non-parmateric that is useful for the ordinal or ranked data sets. It also avoids the normality assumption (imposed by dependant samples t-test).
#### 5. ANOVA (Analysis of variance)
  ANOVA is used to compare the mean of three or more groups to evalute whether they are similar or not. The variation between the means of groups vs the variation within group is the working principal of this test. 
  ```{r}
      anova(weight ~ group, data = data)
      or 
      anova(object)
  ```
where object is the output of model fitting functions such as lm or glm. 
#### 6. Kruskal-Wallis test
  Non-paramtertic test to evalute the statistical significance among the medians of three or more groups using ranks. This is an alternative to one-way ANOVA.
  ```{r}
      kruskal.test(weight ~ group, data = data)
  ```
The group variable contains the different groups such as control, treated1, treated2 etc. 

### **Relationship between variables**
#### 1. Correlation
   The correlation analysis reveals how the two variables behave/change with respect to each other, for instance, if one variable is increasing and other is also increasing in magnitude, they are positively correlated with each other. The correlation can be positive, both are going in the same direction, negative, both varibales are in opposite direction, and no-correlation, increase/decrease in one variable does not influence other variable. The correlation can be measured by either one of two methods:
  a. Pearson: this is default method in R, quite reasonale for linear relationships. In case of non-linear relationships, the correlation strength can degrade.
  b. Spearman: Another way to measure the correlation, however, it can be better in case of non-linear relationships.

Correlation can be measured by "cor" command in base-R, where the default method can be substituited by "method" argument. 
```{r}
cor(vector_1, vector_2, method = "pearson")
```

#### 3. Linear regression
  A statistical method that used to estimate the linear relationship between a dependent variable and one or more independent variables. This method estimate the relationship by fitting a straight line (best fit) to the independent variables. It can be used to predict the value of unknown dependent variable as well as used to interpret the data. In order to perform the linear regression, there are 4 main assumptions that have to be met, otherwise, the results can be spurious.
  (1) IID: Independently acquired idneticficaaly distributed independent values. 
  (2) Normlaity of residuals: The residuals (the difference between the observed and predicted values) are normaly distributed.
  (3) Homoscadascity: The variance of error terms (residuals) should be consistent across all levels of the independent variables.
  (4) Multicolinearity: There should be little or no colinearity in the data. Lack of correlation among the independent variables that can affect the outcome.
  Apart from these, other assumptions such as absence of endogeneity, no outlier etc should also be obbserved. 
  There are various method that can test spurious data such as QQ plot (for normality assumption), VIF (variance inflation factor) to determine the multicolinearity etc. 
  
#### 4. Logistic regression

### **Categorical data**
#### 1. Chi-square test
#### 2. Fisher's exact test

### **Assumption testing**
#### 1. Shapiro-Wilk test
#### 2. Kolmorgorov-Smirnov test

### **Essential concepts**
#### 1. p-values vs confidence interval
   p-value refers to the certainity with that you can reject the null hypothesis. The threshold value can range from 0.1 to 0.001 depending on the objective of the experiment. Usually, 0.05 (or with 5% uncertainity) is used, however, you can tweak this to lower or higher values. A literature search of the relevant domain will provide the usuall threshold.  
   On the other hand, the confidence interval refers to the range where the true-value lies. In other words, a 95% confidence interval of 2.5 to 3.4 means that I am 95% confidence/sure that the true value (mostly p-value or any other statistical measure) lies between 2.5 to 3.4 units. 
#### 2. Effect size
#### 3. Power analysis
#### 4. Outliers and transformation
#### 5. Reproducibility
#### 6. Randomization
