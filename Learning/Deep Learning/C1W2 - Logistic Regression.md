alghorithm for binary classification
logistic regression is a simple form of neural network
### Notation
x is input feature vector, 1 column
so effectively each and every RGB value is its own feature, n<sub>x</sub> is the amount of features
m is the amount of training examples
X is the matrix that holds all the m training examples, m amount of examples(columns), n<sub>x</sub> amount of features(rows), x<sub>shape</sub> = (n<sub>x</sub>, m)
![[Pasted image 20240628161828.png]]
Correspondingly, Y is matrix of all the results(predictions), y<sub>shape</sub> = (1, m)
![[Pasted image 20240628162402.png]]
### main
given x, want $\hat{y} = P (y = 1 | x)$ (probabillity that y is 1 given x)

to compute this we introduce 2 new parameters, 
- $w$ which is a column vector with length $n_x$ 
- $b$ which is a scalar

$w$ is effectively a way for the alghorithm to determine how important each feature is. It is defined as a column vector so that the transpose can make a dot product with x, which in turns gives a scalar value, ie $\hat{y}$ .

$b$ allows the model to adjust the output indepenently of the input features\

This is put together in the linear expression, which, with a correctly fitted w and b, should give a propabillity that y is 1.  

$z = w^T x + b$

This function is then put into the "sigmoid function":
$\hat{y} = \sigma (w^T x + b)$,

The sigmoid function is defined as:
$\sigma(z) = \frac{1}{1 + e^{-z}}$
but it effectively just squashes the result between 1 and 0 to get a nice probability,
![[Pasted image 20240628165356.png]]

To figure out these parameters $w$ and $b$, we are given $m$ training examples (x, y).

### Loss Function
Determines how good our output $\hat{y}$ is given the correct $y$. $L(\hat{y}, y)$
The loss function we use in logistic regression is called binary cross-entropy loss:
$L(\hat{y}, y) = -(y\ log\ \hat{y} + (1 - y)\ log(1 - \hat{y}))$
part of why we use this loss function is because it create a convex cost function with a single minimum
### Cost function
J(w,b). Average of the loss function for all training examples, expresses how good ur parameters are for entire training set, not just 1. need to find w and b that 'minimize' the cost of the parameters
$J(w, b) = \frac{1}{m}\ \sum_{i = 1}^m L(\hat{y}^{(i)}, y^{(i)})$


### Gradient Descent
the graph of (w, b) => J(w, b) is convex so can find the local minimum. 
![[Pasted image 20240618180219.png]]
Gradient descent is the alghorithm that will eventually converge towards the global optimum
in practice this would look something like this:
repeat {
$w := w - \sigma \frac{dJ(w)}{dw}$ = $w - \alpha\ dw$
}
so, continually redefine $w$ with the derivative times $\alpha$, alpha being the learning rate, the derivative being the slope at that point on the function

above example only uses $w$, for the full implmentation it would be something like:
![[Pasted image 20240628182057.png]]

for a single training example then:
gradient descent in logistic regression would then involve, creating derivative formula for dz, then updating w and b like shown above, ie $w := w_1 - \alpha \ dw_1$, $dw_1$ being = $x_1 \ dz$ 
in logistic regression: $dz = a - y$, a being the prediction

$dw_i$ and $db$ for the entire training set or cost function can be determined also by summing the derivatives for all the individial training sets and then $/m$ to find average
### vectorization
vectorization is essentially removing for loops, and using numpy functions instead

in logistrict regression, instead of looping over all the features in each training example, initialize zero array $dw = np.zeros(n_x, 1)$ and then $dw+ = x^{(i)}dz^{(i)}$, x now being the entire input feature vector
#### Z
instead of using for loops u just dotting and multiplying together huge vectors ie:
$Z = [z^1, z^2....z^m]$ = $w^T\ X + [b...b]$
in python: (b is broadcasted)
$Z = np.dot(w.T, x) + b$
#### A 
in python: needs appropiate implementation of sigma
$A = [a^1....a^m] = \sigma(Z)$
#### dZ
$DZ = [dz^1, dz^2...dz^m] = A - Y$   

#### db
$db = \frac{1}{m}\ np.sum(dZ)$
#### dw
$dw = \frac{1}{m}\ X \ dZ^T$

![[Pasted image 20240628193352.png]]
single iteration of gradient descent:. left with for loops, right with full vectorization:
![[Pasted image 20240628193845.png]]

