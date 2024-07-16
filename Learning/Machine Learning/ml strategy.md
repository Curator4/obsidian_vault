## orthogonalization
- seperation of concerns...
- adjusting model by changing specific variables
- early stopping has bad orthoganilization since it affects both training and dev set performance
## goal
- use a singular number $F1$ variable to determine model viability, average of precision and recall
- could also combine optimize and satisfying metric, ie optimize accuracy while runnign time below X, or optimize accuracy while flase positives below 1%
- while satisfying conditions X optimize Y
- make sure ur dev and test set have the same distribution
## comparing to human-level performance
- bayes optimal error = the best possible error rate, (100% accurate model)
- human level performance is often close to bayes
- models tend to improve fast while below human level, but slower after
- can generally think of human level error as estimate of bayes\
- compaing ur accuracy to the human level performance can inform u whether to focus on bias or variance improvement
## error analysis
+ evaluate different ideas for impoving model
+ set up spreadsheet with each problem/idea, assign percentages for selection of mislabeled examples
+ one of these problems could be examples that are mislabeled
+ can give inspiration or help prioritize how to improve model
+ suggested approach = build first system quickly, then iterate with variance/bias analysis and error analysis
## mismatched traning and dev/test set
- when getting more data ie from the web, ie data not from the same distribution as ur dev/test set, the ideal option is to only add it to the training data, not the dev/test sets
- why? cuz the dev test tells the model "where to aim", so the contents of the training data is agnostic to the predictions, what matters is the dev set
- an issue with this is that it can throw off variance analysis between training and dev error, since train and dev sets come from different distributions
- to fix: create a new training-dev set and compare the variances between: training, training-dev and dev, to see where the variance occurs, if u have high variance between train and train-dev, u have high variance![[Pasted image 20240716033728.png]]
- if there is big difference between train-dev and dev, there is a data mismatch problem 
- key quantities:
	- human level
	- training error
	- train-dev error
	- dev error
	- test error ![[Pasted image 20240716034350.png]]
- how to adress data mismatch? no easy systematic process
	- carry out manual error analysis
	- based on analysis, make training data more similar
		- artificial data synthesis, careful of overfitting
	- collect more data similar to dev set
## transfer learning
- the process of using a trained neural network model, removing a amount of layers and using the same weights etc, train the removed layers, possibly add layers, according to new dataset
- useful when both models are within a specific field like image recognition (same input)
- makes sense if u dont have a large amount of data for the new model
- the existing model would then be the 'pre-training' part
- the part of the model u train would be the 'fine-tuning' part ![[Pasted image 20240716041350.png]]
## multi-task learning
- essentially training one nn to do different things
- just a nn with multiple outputs
- can improve performance compared to training one nn in isolation
- different from softmax regression because multiple outputs can be 1 ![[Pasted image 20240716042923.png]]
- makes sense when 
	- several tasks have shared lower-level features
	- amount of data you have for each task is similar
	- when you can train a nn big enough to handle all tasks
- in practice used less than transfer learning
## end-to-end deep learning
- the process of ignoring all intermediary steps, and just going from x -> y
- this is enabled by the existence of a large amount of data so the nn can ignore the steps
- not always applicable, only use if you have sufficient data to learn the complexity x->y
- pros
	- lets the data speak, finds most appropiate x -> y, not forced to reflect human preconceptions
	- less hand-designing of components needed
- cons
	- may need large amount of data, x -> y
	- excludes potentially useful hand-designed components