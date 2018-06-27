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
    epoch += 1
    
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


