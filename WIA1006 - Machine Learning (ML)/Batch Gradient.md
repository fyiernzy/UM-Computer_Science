# Gradient descent

Gradient descent is an iterative optimization algorithm commonly used in machine learning to minimize a cost function. The basic idea is to update the model parameters in the direction of the steepest descent of the cost function. There are three types of gradient descent, namely batch gradient descent, stochstic gradient descent (SGD) and mini-batch gradient descent.

## Batch gradient descent

Batch gradient descent is a type of gradient descent that updates the model parameters based on the average of the gradients of the cost function with respect to each training example in the entire training set. In other words, it computes the gradient of the cost function for the entire training set before taking a step towards the minimum.

## Stochastic gradient descent (SGD)

Stochastic gradient descent (SGD) is another type of gradient descent that updates the model parameters based on the gradient of the cost function with respect to a single randomly chosen training example. Unlike batch gradient descent, it doesn't require computing the gradient for the entire training set, making it much faster and more efficient. However, the convergence can be noisy and may require additional hyperparameter tuning.

## Mini-batch gradient

Mini-batch gradient descent is a compromise between batch and stochastic gradient descent. It updates the model parameters based on the gradient of the cost function with respect to a small batch of randomly chosen training examples (typically between 32 to 512), rather than the entire training set or a single training example. This approach can lead to faster convergence than batch gradient descent, with less noise and better generalization than stochastic gradient descent.

Here are some key similarities and differences between the three gradient descent methods:

Similarities:

1. All three methods are iterative optimization algorithms that update the model parameters based on the gradient of the cost function.
2. They are commonly used in machine learning for minimizing the cost function and improving model performance.

Differences:

1. Batch gradient descent computes the gradient for the entire training set, while stochastic gradient descent computes the gradient for a single training example, and mini-batch gradient descent computes the gradient for a small batch of training examples.

2. Batch gradient descent can be slower and less efficient than stochastic or mini-batch gradient descent, especially for large training sets, while stochastic gradient descent can be noisy and require more hyperparameter tuning.

3. Mini-batch gradient descent is a compromise between batch and stochastic gradient descent and can offer better convergence speed and generalization than either method alone.

Overall, the choice of gradient descent method depends on the size of the training set, the complexity of the model, and the available computational resources. Batch gradient descent is suitable for small datasets, while stochastic gradient descent and mini-batch gradient descent are more efficient for large datasets.
