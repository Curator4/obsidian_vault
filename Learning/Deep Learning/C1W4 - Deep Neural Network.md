### Notation
remember we don't count the input layer, denoted as $l^{[0]}$
$L$ = number of layers
$n^{[l]}$ = units/nodes in layer $l$
$a^{[l]}$ = activations in $l$, etc
$a^{[0]} = x$
$\hat{y} = a^{[L]}$

![[Pasted image 20240707231120.png]]
### matrix dimensions
$W^{[l]} : (n^{[l]}, n^{[l - 1]})$
$b^{[l]}: (n^{[l]}, 1)$
$dW^{[l]}: (n^{[l]}, n^{[l - 1]})$
$db^{[l]}: (n^{[l]}, 1)$
$Z^{[l]} , A^{[l]} , dZ^{[l]} , dA^{[l]}  : (n^{[l]}, m)$
\
### computation
forward and backprop, one iteration of gradient descent
![[Pasted image 20240708000656.png]]
#### forward
![[Pasted image 20240708000954.png]]
#### backward
![[Pasted image 20240708001406.png]]importantly: the derivative of $da^{[L]}$, the final layer which u need to start the backwards propagation is given as (for binary cross-entropy loss): $$da^{[L]} = -\frac{y}{a} + \frac{1-y}{1 - a}$$which is then stacked together to get $dA^{[L]}$

#### extra formulas from assignment
![[Pasted image 20240708014744.png]]
![[Pasted image 20240708022018.png]]
![[Pasted image 20240708022024.png]]
![[Pasted image 20240708023759.png]]
### hyperparameters
parameters: $W, b$
hyperparameters:
- learning rate $\alpha$
- iterations
- hidden layers $L$
- hidden units $n^{[l]}$
- activation functions