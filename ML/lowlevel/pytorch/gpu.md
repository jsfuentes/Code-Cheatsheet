# GPU Optimization

```python
device = "cpu"
if torch.cuda.is_available():
  device = "cuda"
elif torch.backends.mps.is_available() and torch.backends.mps.is_built():
  device = "mps"
```

## MPS

```python
# MacOS 12.3+
print(torch.backends.mps.is_available())
# PyTorch installation built with MPS
print(torch.backends.mps.is_built())

device = torch.device("mps")
```

## CUDA

Check whether GPU accelaration with CUDA available

Simply move inputs, labels, and model to GPU add parallelization and speed, ez

```python
if torch.cuda.is_available():
    a = torch.LongTensor(10).fill_(3).cuda()
```

## Usage

```python
device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")
cuda = torch.device('cuda')     # Default CUDA device
```

#### Model

```python
net.to(device)
```

#### Inputs

At every step

```python
inputs, labels = inputs.to(device), labels.to(device)
```

#### Tensors

Same

```python
d = torch.randn(2, device=cuda2)
e = torch.randn(2).to(cuda2)
f = torch.randn(2).cuda(cuda2)
```

