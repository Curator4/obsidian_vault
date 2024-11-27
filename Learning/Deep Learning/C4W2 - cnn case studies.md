# cnn case studies
## classic networks
### LeNet - 5
- recognizes picture of number
- structure: c -> avg -> c -> avg -> fc -> fc -> softmax
- 60k parameters
### AlexNet
- input rgb image
- structure: c -> max -> c -> max -> c -> c -> c -> max -> fc -> fc -> softmax
- ~60 million parameters
- used ReLU 
### VGG - 16
- simplified architecture by having same hyperparameters
- 16 = 16 layers with eights
- input rgb image
- structure: c -> c -> pool -> c -> c -> pool -> c -> c-> c-> pool -> c -> c-> c-> pool -> c -> c -> c -> pool -> fc -> fc -> softmax
- ~138M parameters
- relative uniformity made it attractive
## resnet
- residual networks
- the a value from a previous layer is injected between the linear/relu parts of another layer further ahead ![[Pasted image 20240719125421.png]]
- helps with the problem of cost functions starting to increase ![[Pasted image 20240719014717.png]]
- a typical residual block would be $$a^{l+2} = g(z^{[l+2]} + a^{[l]})$$
- basically, by adding the $a^{[l]}$ term in the next layer, the model or individual layer will have an easy time getting the same performance as the previous layer, so you can't "get worse"
- because z will just go to 0 and then u have $a^{[l]}$
- z and a need same dimensions here, so typically use the 'same' padding
- or some people use an extra w to transform the dimensions of a to match z, w can be either learned or just be static to 0 padding
- after a pooling layer u typically need to do one of these matrix dimensions adjustments with and extra w
- identity block, input activation has same dimensions as output activation![[Pasted image 20240719125646.png]]
- convolutional block, when input and output dimensions dont match, the difference with the identity block is that there is a CONV2D layer in the shortcut path, The CONV2D layer in the shortcut path is used to resize the input 𝑥 to a different dimension:![[Pasted image 20240719140533.png]]
- ![[Pasted image 20240719144625.png]]
## inception
- a 1x1 convolution can help shrink the number of filters in the a matrix
- instead of choosing yourself which filter-size/pooling to use, you can do them all and stack the result with padding, 1 inception module: ![[Pasted image 20240719022245.png]]
- uses 1x1 convolutions first to reduce computation, creates a 'bottleneck' layer
- an inception network is just several inception modules together, essentially
## MobileNet
- runs with low computational requirements, like mobile phones
- uses depthwise separable convolution, just a convolution that takes less computations
- consts of depthwise convolution -> pointwise convolution ![[Pasted image 20240719024016.png]]
- uses n_c filters, ie each channel has its own filter so rgb = 3, depthwise convolution
- applies x 1x1 filters, pointwise convolution
- mobilenet v1 is just depthwise seperable convolution blocks
- mobilenet v2 uses blocks of expansion -> depthwise -> pointwise(projection), with a residual component. ends with pool, fc, softmax![[Pasted image 20240719025301.png]]
- expansion convolution just a 1x1 convo with tons of filters, used to increase the filter size
- the 1x1 bottlenecks are good for minimizing memory usage in residual passes![[Pasted image 20240719150736.png]]
# practical advice for computer vision

## transfer learning
- transfer learning, use weights from open source etc to start off ur project. means u dont have to train as long
- essentially the weights for ur entire model are pre trained, and then u train the final layer urself, that outputs the softmax, freeze rest of model
- the amount of layers you freeze is proportional to the amount of personal training data you have
- you can also use the whole 'tranfer learning' downloaded model, just as weight initialization if u have a lot of data ![[Pasted image 20240719153418.png]]
## data augmentation
- mirroring
- random cropping
- rotation
- color shifting, messing with the rgb calues
- etc
- get started with someone elses open source augmentations![[Pasted image 20240719150310.png]]
