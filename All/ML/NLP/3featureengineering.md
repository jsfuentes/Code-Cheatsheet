# Feature Engineering
Creating New Features to get most out of data, can be complex topic

## Creating New Features
length
title

#### Check if feature actually important
Lets make some histagrams
```py
from matplotlib import pyplot
import numpy as np
%matplotlib inline

bins = np.linspace(0, 200, 40) #40 #'sfrom 0-200,
pyplot.hist(data[data['label'] == 'spam']['body_len'], bins, alpha=0.5, normed=True) #normed normalized to some scale
pyplot.hist(data[data['label'] == 'ham']['body_len'], bins, alpha=0.5, normed=True)
pyplot.legend(loc='upper left')
pyplot.show()
```
Err on side if leaving feature in model to see if its good

## Transformations
- Why?
- If left skewed, log transformed data pulls it to the middle. Model might dig too much into a tail inside of exploring the differences of the majority.

#### Where
- Prime candiates dramatic skew with long tail or few outliers
- Bimodal isn't heavily skewed without clear outliers

#### Box-Cox Power Transformation
- Usually use exponents, y^x => y is value x is exponent.
- Aim for normal distrubution, dont worry about 0 
- Test range of exponents, get measurement criteria
