# Review of ML

A single layer neural network is capable of representing any function

Most basix is like perception, feed forward neural network

### GANS(Generative Adversarial Networks)

Generator creates images and Discriminator decides whether the images are real or fake. 

## CCN(Convontional Neural Net)

Use a convontial matrix/filter on images instead of using raw pixels as input

## RNN

Recurrent Neural Networks are good for time series data that has a concept of memory, introduces loop back from neurons to make training more efficient

### LSM

Long term short term memory, a neuron has a forget and memory type thing

## Auto-encoders

Like PCA, but neural net trying to learn identity function in small amount of space and for general objects

## How to Train Neural Networks

Grid search, monte carlo, gradient descent, adadelta(change gradient according to sample)

## Activation Function

Adds non linearity which allows neural networks to get any math function

Softmax- for multiple categories

Rlu- max(0, z) less complexity and helps neural nets train faster 

Leaky Rlu - prevents dead neurons by having less than 0 be less than 0 

## Regularization

Penalize complexity, 