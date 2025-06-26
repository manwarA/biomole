---
Title: "What statitical tests are essential to learn for a biologist"
Date: 2025-06-23
Author: MA Anwar
---
There are hundereds of statistical tests that have been proposed over the years for various situations. However, it is not feasible to master all these tests even for statitiion, let alone a biologist should learn these. Here, lets dive into the most prominent tests that are frequently used by biologists and should be learnt for effective research. 

### **Comparing group differences**
1. t-test
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


3. Mann-Whitney U test
4. ANOVA (Analysis of variance)
5. Kruskal-Wallis test

### **Relationship between variables**
1. Correlation
  a. Pearson
  b. Spearman
2. Linear regression
3. Logistic regression

### **Categorical data**
1. Chi-square test
2. Fisher's exact test

### **Assumption testing**
1. Shapiro-Wilk test
2. Kolmorgorov-Smirnov test
3. Levene's test
4. Bartlett's test

### **Essential concepts**
1. p-values vs confidence interval
2. Effect size
3. Power analysis
4. Outliers and transformation
5. Reproducibility
6. Randomization
