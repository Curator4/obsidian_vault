- where is x in the image, as opposed to classification = is x in the image
- localization vs segmentation, localization is finding the bounding boxes of objects, segmentation is labelling each pixel with its corresponding class
- define several other outputs for the network, height, width, coordinates of midpoint
- you can define any landmark you want in ur training data, then train the model to find those datapoints. like specific points in a human face etc
	- landmarks in training data-set mmust naturally have consistent datapoints
	- this is slow tho, so we want a convolutional implementation
- sliding windows is running over the entire image with small boxes, can be done with convolutions instead for increased effeciency ![[Pasted image 20240721012632.png]]
##  YOLO algorithm:
- You Only Look Once
- use the object classification/location model alongside slicing windows algorhithm to find multiple  objects, u assign an objects midpoint (from the classification) to a sliding window frame![[Pasted image 20240721020646.png]]
- very cool object detection algo :D ![[Pasted image 20240722053633.png]]![[Pasted image 20240722053645.png]]
## Intersection over Union (IoU)

calculates interception between predicted and actual bounding box, convention is 'correct' = $\geq 0.5$
- iou is quotient of the area of the intersection, in otherwords, in other words, divide the intersection by the sum of both areas
## non-max suppression
- several grids can detect the same object, how fix? non-max suppresion
- supresses detections with high overlap (IoU), selects for detections with highest Pc prediction
## anchor boxes
- what if 2 different objects overlap in same grid?
- u basically save geometric shapes according to different objects, and then depending on which shape the prediction overlaps with, assign it to that. so each grid stores anchor boxes for object detection
- how do you add these 'anchor boxes'? u extend the neural net outputs, essentially stacking outputs together
- works for only 2 objects?
- there a better way to automatically choose anchor boxes ![[Pasted image 20240721211959.png]]
## R-CNN
- proposes regions using a segmentation algorithm, runs model on suggested regions
- usually slower than yolo algo
## semantic segmentation, U-net
- seperates every single pixel in picture into semantic regions!![[Pasted image 20240721214151.png]]
- to create segmentation output, u need to blow up the convolutional again, instead of decreasing it
- transpose convolution
	- convoluting an array with a kernel/filter that has larger dimensions, outputs a larger matrix
	- a bit like reverse convolutions, look up
	- used becuz it blows up the dimensions
- U-Net, simple![[Pasted image 20240722023710.png]]
	- starts with convolutions, spatial information is lost
	- second half uses transpose convolutions back towards input size
	- unet uses skip connections becuz several types of information are relevant
- U-Net, full ![[Pasted image 20240723010209.png]]
	- classes here is whatever u want as output
	- use sparse categorical crossentropy instead of crossentropy when dealing with lots of classes![[Pasted image 20240723020301.png]]
