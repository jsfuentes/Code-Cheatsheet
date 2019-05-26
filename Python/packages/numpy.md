# Numpy

## Creation

```python
import numpy as np

A = np.array([[1,2,3],[4,5,6],[7,8,9]])
B = np.random.randn(5,1)
C = np.zeros((1,3))
```

### Andrew Ng Tips

- Andrew Ng, call.reshape to document the size you expect things to be, its cheap
- Don't use rank 1 arrays like `np.random.randn(5)` use `np.random.randn(5,1)` , rank 1 won't act as col or row

## Info

`x.shape[0] `

## Operations

### Broadcasting

```python
A = np.array([1,2,3,4])
A + 100 #elementwise addition

A = np.array([[1,2,3], [4,5,6]]) + np.array([[100,200,300]])
#adds 100, 200, 300 to both rows
```

(m, n) +-/* (1,n) 		=> 		(m,n) 

- if either row or col is 1, than that will be expanded to the proper size

### Common ops

```python
np.exp(x) #e^x
np.dot() #matrix mult and 1d*1d dot too
x * y #elementwise. also np.multiply
X.T #transpose
```

## Reducers

- Axis: 
  - 0 is vertical, column 
  - 1 is horizontal, row
  - default is all in 2D
- keepdims keeps it as a matrix instead of collapsing to a 1D vector i.e (x, 1) instead of (x,)

```python
cal = A.sum(x, axis=1, keepdims=True)
minX = np.amin(data, axis=1, keepdims=True)
maxX = np.amax(data, axis=1, keepdims=True)
```

## Reshaping

```python
A = numpy.random.randn(21,21,3)
A = A.reshape((21*21*3, 1)) #One dimension can be -1 to be inferred

#A trick when you want to flatten a matrix X of shape (a,b,c,d) to a matrix X_flatten of shape (b ∗∗ c ∗∗ d, a) is to use:
X_flatten = X.reshape(X.shape[0], -1).T
```

### Normalize

For normalizing machine learning stuff

```python
x = x/np.linalg.norm(x,axis=1,keepdims=True)
```