# Neural Nets

## Model

```python
class LinearRegressor(nn.Module):
    def __init__(self, input_dim, hidden_dim, output_dim):
        super(LinearRegressor, self).__init__()
        self.h1 = nn.Linear(input_dim, hidden_dim)
      	self.h2 = nn.Linear(hidden_dim, output_dim)
        
    def forward(self, x):
        x = self.h1(x)
        x = F.tanh(x)
        x = self.h2(x)
        return F.log_softmax(x)

model = LinearRegressor(1, 1, 1)
```

### Functions

```python
model.zero_grad() #zero grad on all hidden layers(self attrs)
model.parameters() #can iterate over inner layers
```

## Loss & Optimizer

```python
loss_function = nn.MSELoss()

optimizer = torch.optim.SGD(model.parameters(), lr=0.001)
```

## Train 

```python 
epochs = 10000
for epoch in range(epochs):    
    inputs = Variable(torch.from_numpy(x_train))
    
    real_outputs = Variable(torch.from_numpy(y_train))
    
    #reset gradients
    optimizer.zero_grad()
    
    #Forward - compute the output
    pred_outputs = model(inputs)
    
    # Loss
    loss = loss_function(pred_outputs, real_outputs)
    
    #Backword - compute gradients
    loss.backward()
    
    #update parameters
    optimizer.step()
    
    print('epoch {}, loss {}'.format(epoch, loss.data[0]))
```

## Test

```python
def test(network, loss_ft, test_loader, epoch):
    network.eval()
    test_loss = 0
    correct = 0
    with torch.no_grad():
        for data, target in test_loader:
            output = network(data)
            indicator_target = torch.sparse.torch.eye(10).index_select(dim=0, index=target)
            test_loss += loss_ft(output, indicator_target).item()
            pred = output.data.max(1, keepdim=True)[1]
            correct += pred.eq(target.data.view_as(pred)).sum()
    test_loss = (test_loss / len(test_loader.dataset)) * 1280
    test_losses.append(test_loss)
    accuracy = 100. * correct / len(test_loader.dataset)
    test_accuracy.append(accuracy)
    print('\nEpoch {}: Test Avg. Loss: {:.8f}, Accuracy: {}/{} ({:.0f}%)'.format(
    epoch, test_loss, correct, len(test_loader.dataset), accuracy))
```

## Model Examples

```python
class SimpleCNN(nn.Module):
    def __init__(self, in_channels, full_input):
        super(SimpleCNN, self).__init__()
        #torch.nn.Conv2d(in_channels, out_channels, kernel_size, stride, padding)
        self.conv1 = nn.Conv2d(in_channels, 32, 5, 1, 2)
        self.conv2 = nn.Conv2d(32, 64, 3, 1, 1)
        self.conv3 = nn.Conv2d(64, 64, 3, 1, 1)
        self.full = nn.Linear(full_input, 10)
        self.full_input = full_input

    def forward(self, x):
        s1 = self.conv1(x)
        z1 = F.relu(F.max_pool2d(s1, 2))
        s2 = self.conv2(z1)
        z2 = F.relu(F.max_pool2d(s2, 2))
        s3 = self.conv3(z2)
        z3 = F.relu(F.max_pool2d(s3, 2))
        s4 = z3.view(-1, self.full_input)
        z4 = self.full(s4)
        return z4
```

## Intialize Weights

```python
def init_weights(m):
    if type(m) == nn.Conv2d:
        w = torch.empty(*m.weight.data.shape)
        nn.init.normal_(w)
        nm = math.sqrt(2.0/(m.in_channels * m.kernel_size[0] * m.kernel_size[1]))
        w =  w * nm
        m.weight.data = w
        b = torch.empty(*m.bias.data.shape)
        nn.init.constant_(b, 0)
        m.bias.data = b
    elif type(m) == nn.Linear:
        w = torch.empty(*m.weight.data.shape)
        nn.init.normal_(w)
        w =  w * math.sqrt(2.0/w.shape[1])
        m.weight.data = w 
        b = torch.empty(*m.bias.data.shape)
        nn.init.constant_(b, 0)
        m.bias.data = b

MNIST_CNN = SimpleCNN(1, 576)   
MNIST_CNN.apply(init_weights)
```

