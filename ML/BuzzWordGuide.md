# ML BuzzWords Guide

A single layer neural network is capable of representing any function

## Network Types

Most basic is perception, feed forward neural network

#### LLM (Large Language Models)

#### GANS(Generative Adversarial Networks)

Generator creates images and Discriminator decides whether the images are real or fake. 

#### CCN(Convolutional Neural Net)

Use a convolutional matrix/filter on images instead of using raw pixels as input

#### RNN

Recurrent Neural Networks are good for time series data that has a concept of memory, introduces loop back from neurons to make training more efficient

#### LSM

Long term short term memory, a neuron has a forget and memory type thing

#### Auto-encoders

Like Principal component analysis (PCA) in reduce dimensions of data, but neural net trying to learn identity function in small amount of space and for general objects

## Training Methods

Grid search, monte carlo, gradient descent, adadelta(change gradient according to sample)

Regularization penalizes complexity

#### Batch Gradient Descent

Batch of 1(stochastic gradient) doesn't use vectorization well and so can be slower than larger batches

Batch of m is too slow for large m. If less than say 2k, just do batch. 

Else your minibatch should fit in Cpu/gpu mem and often good as a power of 2 like 128, 256, or 512.

## Activation Function

Adds non linearity which allows neural networks to get any math function

Softmax- for multiple categories

Rlu- max(0, z) less complexity and helps neural nets train faster 

Leaky Rlu - prevents dead neurons by having less than 0 be less than 0 

