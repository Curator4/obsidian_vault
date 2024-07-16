### General

**Reminder**: The general methodology to build a Neural Network is to:

```
1. Define the neural network structure ( # of input units,  # of hidden units, etc). 
2. Initialize the model's parameters
3. Loop:
    - Implement forward propagation
    - Compute loss
    - Implement backward propagation to get the gradients
    - Update parameters (gradient descent)
```
![[Pasted image 20240706232019.png]]
### Layers
basic layers look like this ![[Pasted image 20240706165750.png]]
the hidden layer is called so because the training set has no values for it.
$a^{[0]}$, First layer also called the input layer, denoted as $a^{[0]}$
$a^{[1]}$, Hidden layer denoted as $a^{[1]}$, with individial layers being known as ex. $a^{[1]}_1$. column vector.
$a^{[2]}$, Output layer, outputs scalar value $\hat{y}$, 
the conventional notation is $a^{[l]}_i$ , $l$ being the layer and $i$ being the node in the layer

layers 1 and 2 have variables connected to them also defined by the subscript. 
$w^{[1]}$ has shape (4, 3) here since there are 4 hidden nodes and 3 input features.

even tho this has 3 layers, the convention is that this would be called a 2 layer NN, since input layer doesnt count

each node effective represents the 2 typical logistic regression steps with their respective variables  ie:
1. $z = wx + b$
2. $a = \sigma(z)$

### Vectorization
x is alias to $a^{[0]}$
![[Pasted image 20240706232307.png]]
![[Pasted image 20240706232459.png]]
![[Pasted image 20240706234114.png]]
![[Pasted image 20240706235603.png]]
![[Pasted image 20240707001217.png]]
![[Pasted image 20240706172046.png]]
the computations for multiple training examples can be vectorized similarly to LR.
We then use the similar capital notation like $X$ , $Z^{[1]}$, $A^{[1]}$ , to denote the corresponding values and vectors stacked horizontally. 
Horizontal = training examples, vertial = nodes/features
![[Pasted image 20240706174454.png]]
So effectively, instead of looping through the training examples 1 by 1 we can can compute each of the steps vectorized

### Activation Function
so far the sigmoid function has worked as our activation function, but it can be replaced by other functions if they work better, like $tanh(z) = \frac{e^z - e^{-z}}{e^z + e^{-z}}$, which centers the data around (-1, 1) instead of (0, 1). almost always strictly superior except for maybe output layer
the activation function can be anonymously refered to as g(z), and for each layer $g^{1}(z)$ etc
Other activations functions are $RelU$ and leaky version. learns faster.
![[Pasted image 20240706183628.png]]
most commonly used is the $RelU$ activation function
$a = max(0, z)$

### Gradient Descent
Formulas for calculating the derivative expressions:
$dZ^{[2]} = A^{[2]} - Y$ 
$dW^{[2]} = \frac{1}{m} dZ^{[2]}A^{[1]T}$
$db^{[2]} = \frac{1}{m} np.sum(dZ^{[2]}, axis = 1, keepdims = True)$
$dZ^{[1]} = W^{[2]T} dZ^{[2]} * g'^{[1]}(Z^{[1]})$
$dW^{[1]} = \frac{1}{m} dZ^{[1]} X^T$
$db^{[1]} = \frac{1}{m} np.sum(dZ^{[1]}, axis = 1, keepdims = True)$

Always use random initialization for w so the nodes aren't symmetric, use small numbers for faster learning (with tanh or sigmoid), b can be zeros, could use other numbers than 0.01
$W^{[1]} = np.random.randn((2, 2)) * 0.01$
$b^{[1]} = np.zeros((2,1))$


