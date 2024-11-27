## mini-batch gradient descent
+ you will only take 1 step of gradient descent per iteration on the whole dataset
+ this means if u have gigantic dataset, gradient descent will take comparatively long
+ to fix this problem u can increase the rate of gradient descent by segmenting the training set into mini-batches, also called <b>mini-batch gradient descent</b>
+ pretty much everyone uses this on large sets
+ gives u a new hyperparameter to configure, <u>batch-size</u>
+ typical mini-batch sizes:
	+ 64, 128, 256, 512, 1024 (power of 2)
- make sure minibatch fits in cpu/gpu memory for optimal performance
- an <u>epoch</u> is one pass through the entire training set, ie all the mini-batches
- worse at utilizing vectorization (so takes longer) ![[Pasted image 20240710012608.png]]
### stochastic gradient descent
- mini batch gradient descent when the size of the batch is 1 training set, so updates the weights etc for each training example
### batch gradient descent
- mini batch gradient descent where the batch size is the whole training set
## gradient descent algorhitms
### exponentially weighted averages
- basically, a way to create an 'average' based on previous values, the weights of the previous values are determined by an exponential curve, so the further away from the current training example, the less important it will be in the calculation of the ewa
### gradient descent with momentum
- **Concept**: Momentum adds a fraction of the previous update to the current update. This helps accelerate gradients vectors in the right directions, thus leading to faster converging.
- gradient descent using ewa, essentially, instead of updating with dw and db, u update with $Vdw$ and $Vdb$ that have been averaged using ewa
- effectively smooths out the gradient descent
- introduces new hyperparameter $\beta$, momentum, which controls the ewa, ie how many previous points are weighted, example:
	- $\beta = 0.5$ last 2 or 3 gradients
	- $\beta = 0.9$ last 10 gradients
	- $\beta = 0.98$ last 50 gradients
- Common values for 𝛽 range from 0.8 to 0.999. If you don't feel inclined to tune this, 𝛽=0.9 is often a reasonable default.
- has 2 formulas, one that tunes $\alpha$ one that doesnt, prefers one that doesnt, ![[Pasted image 20240709164339.png]]
- almost always works better than standard gradient descent
- **Advantages**: Helps in smoothing the updates, can escape local minima, and converges faster.![[Pasted image 20240710013846.png]]
- ![[Pasted image 20240710014615.png]]
### RMSprop
- **Concept**: RMSprop adjusts the learning rate for each parameter individually based on the moving average of squared gradients. This helps to deal with the problem of diminishing or exploding gradients.
- similar to momentum, dampens osciliation in gradient descent
- speeds up learning
- **Advantages**: Works well for online and non-stationary problems, and is suitable for handling noisy gradients.
### adam optimization (Adaptive Moment Estimation)
- **Concept**: Adam combines the advantages of both Momentum and RMSprop. It computes adaptive learning rates for each parameter by using estimates of first and second moments of the gradients.
- **Advantages**: Combines the benefits of Momentum and RMSprop, leading to faster convergence and better performance on a wide variety of problems.
- **hyperparameters**, $\alpha$ you need to tune but rest can often be set to default values 
	- $\alpha, \beta_1, \beta_2, \epsilon$ ![[Pasted image 20240710015000.png]]

### Differences
- **Momentum** focuses on accelerating updates by considering past gradients.
- **RMSprop** scales the learning rate of each parameter based on recent gradient magnitudes.
- **Adam** integrates both momentum and adaptive learning rates for a more robust optimization process.

## learning rate decay
- the practice of gradually decreasing the learning rate, $\alpha$ as you get closer to the minimum
- many different versions
	- exponential learning rate decay ![[Pasted image 20240710021424.png]]
	- fixed interval scheduling 
	- ![[Pasted image 20240710021708.png]]
- can also be done manually (set $\alpha$ as model is training)
- speeds up training

## local optima
- basically not an issue because of the very high dimensional space
- creates 'saddle' points not typical local optima
- bigger problem is getting stuck for long time on 'plateaus', a problem which the optimization alghorhitms help with