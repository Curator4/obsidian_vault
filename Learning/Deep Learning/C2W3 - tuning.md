## hyperparameter tuning
- tier 1
	- $\alpha$, the learning
- tier 2
	- $\beta$ , momentum term ~ 0.9
	- mini-batch size
	- hidden units
- tier 3
	- layers
	- learning rate decay
	- $\beta_1, \beta_2, \epsilon$, adam variables, defaults are fine ie. $0.9, 0.999, 10^{-8}$
- random sampling over appropiate scale generally ideal
- $\alpha$and $\beta$ should likely use logarithmic scale
## batch normalization
- normalizes mean and variance a (z) to make it faster to calculate next w and b
- applies the batch norm function before the activation function $Z -> \tilde{Z} -> g(\tilde{Z})$
- batch norm variables specific to each layer, but also different for each node
- works with vectorized on mini batches
- adjusts $d\beta$ and $d\gamma$ aswell in the backprop, (eliminates $db$)
- essentially, w and b will change the values ie weights of the nodes, but applying batch norm ensures that the mean and variance between the nodes in one layer remain the same, adjusted by $\beta$ and $\gamma$
- reduces the problem of input values changing, aka covariant shift
- reduces coupling between layers, allowing each layer to learn more indepently, speeds up learning, especially in later layers
- naturally causes slight noise over different mini-batches, which has the added effect of slight regularization (since later layers cant rely on earlier layers to the same degree)
- at test time for the whole model then, u use estimates for $\mu$ and $\sigma$ (mean and variance), calculated during training using exponentially weighted average from every mini-batch
## softmax regression
- generalizes logistic regression to C classes
- classifies inputs into multiple different classes C
- C units in the output layer, each giving the probability that the input is class X
- uses a particular activation function at layer L that gives that probability
- softmap gives probabilities vs hard max that just outputs 1 for the most likely and zeros