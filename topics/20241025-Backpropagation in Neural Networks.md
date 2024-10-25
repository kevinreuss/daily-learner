# Backpropagation in Neural Networks 

Backpropagation, short for "backward propagation of errors," is a method used in artificial neural networks to calculate the gradient of the loss function with respect to the weights. 

## Algorithm
The algorithm follows four main steps:

1. **Forward Propagation**: Input vectors are fed into the network and propagate through each layer until it reaches the output layer. This output is then compared with the desired output to produce an error value.

2. **Computing Local Gradients**: Local gradients are calculated for every neuron in the network. For output layer neurons, the local gradient is the derivative of the activation function multiplied by the error. 

3. **Backward Propagation of Errors**: Errors are propagated back through the network. The error for each neuron is calculated as the product of the neuron's local gradient and the sum of the errors of all neurons that use it as an input, weighted by the corresponding connection weights.

4. **Adjusting Weights and Biases**: Based on these computed errors, weights and biases are then updated to minimize the cost function.

## Python Implementation
Here's a basic implementation for a neural network with one hidden layer:

```python
def backpropagation(X, y, weights, bias, learn_rate):
    # Forward propagation
    h = 1 / (1 + np.exp(-(np.dot(X, weights[0]) + bias[0])))
    y_hat = 1 / (1 + np.exp(-(np.dot(h, weights[1]) + bias[1])))
    error = y - y_hat

    # Backward propagation
    d_weights2 = np.dot(h.T, (2*(y - y_hat) * sigmoid_derivative(y_hat)))
    d_weights1 = np.dot(X.T,  (np.dot(2*(y - y_hat) * sigmoid_derivative(y_hat), weights[1].T) * sigmoid_derivative(h)))

    # Updating the weights
    weights[1] += learn_rate * d_weights2
    weights[0] += learn_rate * d_weights1
    return weights
```

This code uses the sigmoid function as the activation function, which is differentiable and makes it easy to calculate gradients.

## Summary
Backpropagation is the cornerstone of learning in neural networks. It calculates the gradient of the loss function with respect to the weights, which is then used in gradient descent to update the weights and biases, minimizing the cost function.

For more information, refer to the [Wikipedia page](https://en.wikipedia.org/wiki/Backpropagation).
