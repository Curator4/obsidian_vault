# rnn
- data in a sequence, examples
	- speech recognition
	- music
	- sentiment classification (star rating)
	- dna sequence analysis
	- machine translation
	- video activity recognition
	- name entity recognition
- basic architecture,  equal number of inputs/outputs, many-to-many![[Pasted image 20240725050702.png]]
- there are 3 seperate weights for each layer, $w_x$ , $w_y$, $w_a$ and biases $b_y$, $b_a$ 
- these parameters are then the same for all layers
- this architecture can be changed to fit many-to-one or one-to-many, etc
- full computations with backpropagation through time: ![[Pasted image 20240725051617.png]]
-  other architectures: ![[Pasted image 20240725063409.png]]
- this basic rnn architecture has a weakness of vanishing gradients, ie the backprop has a hard time reaching the early parameters![[Pasted image 20240826184040.png]]![[Pasted image 20240826233525.png]]
# language model
- decides on sentences that make 'sense'
- trains on large corpus of text with an rnn
- since the network is trained to predict words, u can sample sequences from it
- can also be trained on characters, ur vocabulary is just the characters, bad at long range dependencies, computationally expensive
## GRU
- gated recurrent unit
- gru helps significantly with vanishing gradient problem
- allows language model to have long range dependencies
## LSTM
- long short-term memory 
- each gate is a sigmoid function that functions a mask to determine what information to pass on
- top line is the cell state, represents <b>long term memory</b>, modified primarily by forget gate
- the bottom line is the hidden state and handles <b>short term memory</b> 
- each gate has weights for hidden state and input
- forget gate is a sigmoid so it is a tool to reduce or keep the long term memory
- update gate together with the tanh updates the long term memory, determines potential long term memory to remember, the tanh produces a candidate value and update determines how much it carries over, also sometimes called input gate
- final output gate then determines potential short term memory to remember, outputs the next hidden state, the cell state is carried on, prediction is calculated using the hidden state
- ![[Pasted image 20240726021249.png]]![[Pasted image 20240726021324.png]]
- basically passes along a matrix, memory cell, that stores 'memory'![[Pasted image 20240826224459.png]]
# bidirectional rnn (BRNN)
- sometimes a sequencemodel needs information or memory from later parts of the network
- run an extra forward propagation from the 'right to left'
- allows information to pass to the prediction from both the past, present and future
- also works with gru/lstm
- disadvantage: needs entire sequence before you can process it
- 