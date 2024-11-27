# face recognition
![[Pasted image 20240724044954.png]]
## face verification
- "Is this the claimed person?"
- needs one-shot learning, ie learning data from one employee id image
- can use a similiarty function isntead, compare differences between 2 pictures. $$d(img1, img2)$$
- this solves the one shot learning problem
- 1:1 matching problem.
## face recognition
- "Who is this person?"
- 1:K matching problem.
### siamese network
- like siamese twins
- basically, the network given a face outputs a vector (encoding). if it is given the same face the difference between the vectors will be very small. that is how the system recognizes faces, by having a stored database of vectors to compare with
- parameters are learned so that pictures of same person have small difference and pictures of different people have alrge difference
- trained with triplet loss function, anchor, positive and negative.
- another approach is to just use binary classficiation at the end of the siamese network ![[Pasted image 20240724030519.png]]
# neural style transfer
![[Pasted image 20240724054057.png]]
- "generate x in the style of y"
- initiates g (output picture) randomly
- use gradient descent to minimize j(g), adjust g
- j(g) is combination of cost function for x (content, c) and y (style, s)
- the 'style' is defined as the activations of an arbitrarily chosen layer, usually the middle
- content ![[Pasted image 20240724050604.png]]
- style, uses a gram vector to determine the prevalence of patterns of filter on image ![[Pasted image 20240724052824.png]]![[Pasted image 20240724053000.png]]
# 1D, 3D convolutions
- literally same