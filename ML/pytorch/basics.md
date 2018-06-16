## Packages

```python
import torch #similar to numpy
import torch.autograd #differntiation lib
import torch.nn # neural networks lib with autograd integration
import torch.optim # standard op methods like gradient descent

torch.manual_seed(123)
```

## Tensors

Tensors are basically just vector/matrixes

### Creation

```python
torch.empty(5,3) #uninitialized 5*3
torch.rand(5,3)
torch.zeroes(5, 3, dtype=torch.long)
```

From Data

```python
v = [1,2,3]
v_tensor = torch.Tensor(v)
```

### size

- .size()
- .shape()

### Operations

Standard numpy indexing i.e x[:, 1]

#### Cat

```python
x_1 = torch.randn(2, 5) 
y_1 = torch.randn(3, 5)
z_1 = torch.cat((x_1, y_1)) #0 is along first listed axis, 1 2nd etc
```

#### Reshape

```python
x = torch.randn(3200, 3, 28, 28) #3200 photos of 28*28 RGB
# We want a batch, infer second dimesion with -1
x_reshaped = x.view(32, -1, 3, 28, 28) 
print(x_reshaped.shape)
```

### Numpy

They share their underlying memory locations so a change to one will change the other

```python
a = torch.ones(5)
b = a.numpy()
a.add_(1)
print(a)
print(b)
```

Out:

```
tensor([ 2.,  2.,  2.,  2.,  2.])
[2. 2. 2. 2. 2.]
```

## Computation Graphs and Automatic Differentiation

Not fixed like in other things like tensorflow
autograd. Variable keeps track of how it was created

```python
# Variables wrap tensor objects
x = autograd.Variable(torch.Tensor([1,2,3]), requires_grad=True)
y = autograd.Variable(torch.Tensor([3,4,5]), requires_grad=True)
z = x + y
print(z.data)
```

- You can access data with .data attr
- Can do all operations with x autograd 

### See comp graph

```python
operation= z.grad_fn
print(operation)

s = z.sum()
print(s)
print(s.grad_fn)
```

S knows enough about itself to determine its derivative
**backpropagation** calculates gradients with respect to every variable. `.backward` Run backprop starting from it, running multiple times will accumulate it in .grad  prop below. Must keep in data autograd to do grad stuff

```python
s.backward(retain_graph=True)

print(x)
print(x.grad) #value if we differentiate
print(y.grad)
```

### CUDA

Checks whether GPU accelaration with CUDA available
add .cuda function to get it

```python
if torch.cuda.is_available():
    a = torch.LongTensor(10).fill_(3).cuda()
```