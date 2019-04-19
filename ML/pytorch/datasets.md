# Datasets

```python
import torch
import torchvision
```

## Simple

```python
cifar_trainset = datasets.CIFAR10(root='./data', train=True, download=True, transform=None)
cifar_testset = datasets.CIFAR10(root='./data', train=False, download=True, transform=None)
```

## DataLoader

Can be used on datasets 

- `batch_size`, which denotes the number of samples contained in each generated batch.
- `shuffle`. If set to `True`, we will get a new order of exploration at each pass (or just keep a linear exploration scheme otherwise). Shuffling the order in which examples are fed to the classifier is helpful so that batches between epochs do not look alike. Doing so will eventually make our model more robust.
- `num_workers`, which denotes the number of processes that generate batches in parallel. A high enough number of workers assures that CPU computations are efficiently managed, *i.e.* that the bottleneck is indeed the neural network's forward and backward operations on the GPU (and not data generation).

```python
batch_size_train = 64
batch_size_test = 1000
train_loader = torch.utils.data.DataLoader(
  torchvision.datasets.MNIST('./MNIST', train=True, download=True,                       transform=torchvision.transforms.Compose([                     torchvision.transforms.ToTensor(),                           torchvision.transforms.Normalize((0.1307,), (0.3081,))])), batch_size=batch_size_train, shuffle=True)

test_loader = torch.utils.data.DataLoader(
  torchvision.datasets.MNIST('./MNIST', train=False, download=True,           transform=torchvision.transforms.Compose([           torchvision.transforms.ToTensor(),                         torchvision.transforms.Normalize((0.1307,), (0.3081,))])), batch_size=batch_size_test, shuffle=True)
```

## Usage

```python
for batch_idx, (data, target) in enumerate(train_loader):
```

