---
title: Statistic
---

# 1. Adversarial Validation

## 1.1 KS test

```python
# https://www.kaggle.com/code/carlmcbrideellis/what-is-adversarial-validation/notebook

from scipy import stats
features_list = X_test.columns.values.tolist()
for feature in features_list:
    statistic, pvalue = stats.kstest(X_train[feature], X_test[feature])
    print("p-value %.2f" %pvalue, "for the feature",feature)
```

# 2. Loss function

## 2.1 Lightgbm focal loss

```
# https://maxhalford.github.io/blog/lightgbm-focal-loss/
```
 
# 3. Compare performance 

## 3.1 Metric Processing Time

```
https://www.kaggle.com/code/rohanrao/amex-competition-metric-implementations
```




