# convolutions
- convolution is a matrix operation, takes the elementwise product of segments of original matrix using a filter, continually shifting the filter
- useful for edge detection in computer vision
- different filters allow u to find different edges, eg. horizontal vs vertical
- the numbers in the filter can be weights in a neural network
- also called 'cross-correlation' ![[Pasted image 20240718030216.png]]
#### padding
- 'pad' is adding extra pixels on the side, ie 6x6 -> 8x8 ![[Pasted image 20240717051513.png]]
- this does 2 things:
	- prevent the loss of information from the edges
	- makes it so the resulting image retains the dimensions
- 2 most common paddings are
	- p=0, "Valid",
	- $p = \frac{f - 1}{2}$, padding so the output is same size, "Same"![[Pasted image 20240717052221.png]]

#### stride
- stride denotes the shift of the filter after every element-wise product
#### dimensions 
- output dimensions ![[Pasted image 20240717052842.png]]
- convolutions: ![[Pasted image 20240717080008.png]]
- pooling: ![[Pasted image 20240718025055.png]]
#### RGB
- since images have depth 3 due to colors, u apply a 3 depth filter aswell ![[Pasted image 20240717053952.png]]
- u can then use a custom filter to select for different colors etc, or just use same on all colors
- gives a 2d output
#### combining filters
- different filters can be combined after, ie horizontal, vertical
- each filter gives a 2d matrix which u can then combine into 3d matrix 
- resulting matrix has depth = number of filters ![[Pasted image 20240717054512.png]]
- this part confused me a bit, the difference between $n_C$ and $n\_C\_{prev}$. 
	- channels = depth
	- n_C_prev is the amount of channels in the input layer, this matches the amount of channels in the filter
	- n_C is the amount of channels in the output layer, and directly corresponds to the amount of filters, why? because each filter outputs only a single channel. these channels are then stacked for the full output
# cnn
## cnn notation
![[Pasted image 20240717060939.png]]
## layers
### convolution layer
- the "weights" here are the numbers inside the filter ![[Pasted image 20240717055718.png]]
- multiple of these can then be done in succesion which is called a cnn
- each layer can use different filter sizes, padding, stride etc.
- will generally reduce the matrix more and more, increading depth, untill you can unrow and transform it into 1 vector, which u can then use a softmax etc
### pooling layer
- instead of doing a convolution, you can do another operation, like max() or average()
- hyperparameters: $f$ and $s$
- has no parameters to learn
- useful for reducing the matrix, reducing computations etc. 
- pooling layers are usually not counted as their own layers since they have no weights
### fully connected layer
- just a normal neural network layer, occurs near the end of a cnn
### example
- you can then combine convolutional and pool layers to build a network
- near the end the matrix will unrow into a vector, at which point you continue as in a normal nn![[Pasted image 20240717064140.png]]
- a common pattern would be something like conv-pool-conv-pool-fc-fc-fc-softmax
# why convolutions
- faster since a lot less parameters, effectively reduces thes model first before applying a neural network
- parameter sharing
	- essentially, instead of parameters for every single pixel u put parameters in the filters, which can then apply to the whole image
	- each filter can work as a 'feature detector' for the whole image
- sparsity of connections
	- instead of each output value (activation) depending on every single input feature, it now only depends on the features inside the filter
	- so the connections between features is greatly reduced
- essentially it is just putting a bunch of convolutional/pooling layers in phase 1, and then the normal neural network layers afterwards: ![[Pasted image 20240717065945.png]]