## word representation
### word embeddings
- every word in your vocabulary has an accompanying vector of tons of features, the difference between the features of different words helps alghorithm determine context
- can be used to train a nn instead of the one-shot vectors
- information learned from training on massive amounts of internet data can easily be used in transfer learning for ur own training set
- can recognize anologous relationships like man:woman, boy:girl; yen:japan, ruble:russia
- <b>cosine similarity</b> is a way to measure the similarity between two different words![[Pasted image 20240828042305.png]]![[Pasted image 20240828042441.png]]![[Pasted image 20240828044552.png]]
- the embedding matrix is just the feature vectors for all words stacked alongside each other, shape(features, vocab), example: (300, 10,000)
- one shot vector times the embedding matrix gives the embedding for a single word

## word embedding learning algos
 
These are types of word embedding learning algorhitms. they shouldn't rly be relevant since you just download E
- <b>skipgram</b> takes a (random) context word and sometimes random target to train embeddings with $E$ and $softmax$ 
- softmax is expensive to calculate
- <b>negative sampling</b>, another way to traind word vectors. picks a context pair, picks negative pairs at (random). trains with logistic regression
- these are actually used together as in negative sampling is just a technique to make skripgram better

- learning these word embedding training algos is important if you are working in a specific field with specific nomenclature, as opposed to generalized language from wikipedia etc![[Pasted image 20240828055946.png]]
### GloVe
- global vectors for word representation
- it creates dense vector representations of words by analyzing their co-occurrence statistics in a large corpus of text. The goal is to capture semantic meaning and relationships between words, so that words with similar meanings are close together in the vector space.
## sentiment classification
- look at text and classify whether it is positive or negative etc
- rnn with word embedding and then softmax at end for say 1/5 stars is ideal
## debiasing word embeddings
- how to eliminate problematic bias like man: computer programmer, woman: homemaker
- fix wrongful bias for gender, ethnicity, age, sexual orientation, socioeconomic status
- how to reduce problematic bias
	- identify bias direction ie: direction = e.male - e.female
	- neutralize:  project that difference onto words that are not definitional like doctor, programmer, babysitter etc.
	- equalize pairs, make pairs like father, mother equidistant from the axis