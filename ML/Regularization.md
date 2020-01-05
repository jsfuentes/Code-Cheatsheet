# Regularization

Regularization L2's derivative is W so you subtract W from W*learning rate causing **weight decay**

Regularization makes cost perhaps not monotonically decrease. 

#### Dropout regularization 

- Have a keep prob for each layer and randomly drops nodes 
- Mathematically similar to L2 regularization and makes sure network can't depend on one node
- Should always check J decreasing, but dropout makes it more jank. Test code works without dropout and check graph is decreasing. Then add dropout and pray.

#### Early Stopping

plot Dev vs training error and stop early before Dev error increases, basically smaller W regularization with effort of trying different lambda, against orthogonality 

#### Orthogonalization

so many hyper parameters 

#### Weight Intialization

You want smaller weights the more weights

`Randn * sqrt(2/neurons in that layer)` is a good appriozimiation giving you good variance and size