## setup
### train/dev/test sets
- something like 70/30 or 60/20/20 was best practice in past
- nowadays u just need "enough" for last 2 so something like 98/1/1 is fine, or use dev as test set
### bias & variance
- high bias = doesnt fit the training set well, 15%/16%
- high variance = big difference between train/dev prediction (overfitted), 1%/11%
### basic recipe
- high bias? (training performance) -> <u>bigger network</u>, train longer, architecture
- high variance? (dev performance) -> <u>more data</u>, regularization, architecture
bigger network almost never worse, just more computation
### initialization
![[Pasted image 20240709024752.png]]
![[Pasted image 20240709025234.png]]
normal distribution better, avoids values close to extremes
![[Pasted image 20240709025728.png]]
he init just being times with this expression:
![[Pasted image 20240709025806.png]]
### loss function
- **MSE** Mean squared error is used for **regression** tasks, penalizes larger errors more due to squaring, and is sensitive to outliers.
- **Cross-Entropy Loss** is used for **classification** tasks, interprets outputs as probabilities, and measures the performance of the predicted probability distribution against the true distribution.
## regularization
- regularization reduces overfitting ![[Pasted image 20240709041656.png]]
### L2
- $L_2$ regularization (weight decay) for neural nets: $$L_{regularized} = L_{loss} + \frac{\lambda}{2m}\sum_{l=1}^L ||W^{[l]} ||^2 $$
	- it adds a penalty term to the loss function that punishes large weights, so that the overall model doesn't get strongly fitted on statistical outliers
	- effectively, we just redefine the loss function to something that penalizes outlier W values
	- why does this work? cuz of proportational penalty, eg 0.1 x 10 vs 0.1 x 100. they both shrink but one shrinks way more than the other proportionally
	-  lambda being another hyperparameter u have to figure out urself, higher lambda penalizes higher values more ![[Pasted image 20240709034236.png]]
### dropout
- dropout regularization which removes nodes in the network
	- why does that work? cant rely on any one feature, so have to spread out weights
	- effectively that shrinks the weights
	- can vary how many of the nodes u keep depending on the layer 
	- You should use dropout (randomly eliminate nodes) only in training. ![[Pasted image 20240709041557.png]]
### data augmentation
- data augmentation, ie transform picture data, flip etc for more data
### early stopping
- early stopping, test on dev set as you train, stop when reach minimum for less overfitting
	- use the others first as this decreases training
	- bad orthogonalization(does 2 things at once) ![[Pasted image 20240709012644.png]]

## optimization
### normalization
- changes or 'normalizes' the input features to similar ranges for cleaner output
	1. subtract mean
	2. normalize variance
- gives more symmetric cost function graph
### vanishing/exploding gradients
- deep networks can have this problem, especialy with x values close to 1
- naturally causes the gradient descent to take ages if vanishing or suck if exploding
- can reduce this problem with W initialization (relu) $$W^{[l]} = np.random.randn(shape) * np.sqrt(\frac{2}{n^{[l - 1]}})$$
- could also use this initialization variance as a hyperparameter, but not that important comparatively
### gradient checking
- approximate the slope numerically and compare to gradient to check correctness![[Pasted image 20240709015611.png]]
- computation:
	1. define $\epsilon = 10^{-7}$ or similar
	2. reshape all W, b into $\theta$ so $J(\theta)$
	3. reshape all the dw, db into $d\theta$
	4. loop all $\theta$ with formula for approx
	5. compare to $d\theta$
- only used to debug backprop
- doesnt work with dropout since no easily defined J ![[Pasted image 20240709051038.png]]