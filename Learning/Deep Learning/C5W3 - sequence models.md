# encoder/decoder model
- nn outputting a sequence. used for example in translation models
- first trains a encoder network, which encodes the input sentence/image/etc, and a decoder network that generates the output from the decoding
- this entire structure is the rnn model, the beam search is a search strategy used with the decorder to infer the most likely output
![[Pasted image 20240910121622.png]]
- fundamentally the decoder is similar to a standard language model network, but instead of using just a vector of all zeros as the first weights, it uses the output of the encoder network:
![[Pasted image 20240910110844.png]]
- biggest difference is that we dont want to generate a sentence at random, but want the most accurate translation, to facilitate this we can use <b>beam search</b> 
- <b>greedy search</b> is an inferior version that evaluates each word sequentially to see what is most likely
## beam search
- most widely used algo
- the model wants to predict the most likely sentence, the possible sentences are $vocab^{words}$, so with a vocab of 10,000 the amount gets ridiculous.
- greedy search goes through sequentially and takes the most likely word each time, so has only 1 option per word, but predictions suck
- so the options for each are:
	- no search algo: $vocab^{words}$
	- greedy search: $words$
	- beam search: $words^B$
- beam search is functionally similar, it uses a variable $B$, beam width, that determines how many options to evaluate. It goes through sequentially and for each word takes the $B$ most likely next words. It does this for each word, effectively creating a spanning tree that has 3 nodes for every step
- $B = 1$ is effectively the same as greedy search ![[Pasted image 20240910115453.png]]
- uses log to normalize to avoid rounding errors and underflow, since the probalities are very small
- can also normalize by taking average of sentence lengths for each beam or fraction of average, helps combat the preference for short sentences
- bigger $B$ better result, but more computation, not uncommon to see $B = 10$, sometimes researches etc use $B = 1000$ or $B = 3000$, but it has diminishing returns
### error analysis
- to see if the problem is in either the RNN (RNN is both encoder and decoder) or the beam search, we can compare human and algorhitm translations
- basically, the human (correct) translation is always within the the possible outcomes, by comparing the P for the correct translation and the P for the bad translation, we can tell if the problem is the RNN or the beam search. Problems with beam search essentially just means the beam search algo doesnt search wide enough to find the sentence with the highest P
- $P(y^* | x)$ is the output probability of the correct human translation
- $P(\hat{y} | x)$ is the incorrect output of the bad machine translation
- Case 1: $P(y^* | x) > P(\hat{y} | x)$ , beam search chose $\hat{y}$ itself, but $y^*$, which is within the number of possible options, gives a higher P, so this means the beam search is at fault. It didn't search whidely enough to find $y^*$ and we need to increase $B$
- Case 2: $P(y^* | x) \leq P(\hat{y} | x)$ , the correct output has a lower P then the one chosen by beam search. This means that the model itself gave the wrong output, which means the fault lies with the RNN, ie add more data, regularize etc
## Bleu score
The BLEU (Bilingual Evaluation Understudy) score is a metric used to evaluate the quality of machine-generated translations by comparing them to human reference translations. It measures how many n-grams (e.g., words or sequences of words) in the machine-generated translation match those in one or more reference translations.
### Key Points:
- **Purpose:** Evaluates translation quality by comparing the overlap of n-grams (typically up to 4-grams) between the machine-generated output and reference translations.
- **Precision-Based:** Calculates precision for various n-gram lengths and combines them into a single score, with a penalty for translations that are too short.
- **Range:** The BLEU score ranges from 0 to 1, where a higher score indicates better translation quality. A score of 1 would indicate a perfect match with the reference translations.
- **Common Use:** Widely used in natural language processing and machine translation evaluations.
In essence, BLEU provides a quantitative measure of how closely a machine-generated translation aligns with human reference translations.

# attention model
- encoding/decoding has issues with longer sentences say 30-50 words because the encoding has difficulty to memorize such a long sentence, attention model fixes this (blue is encoding, green is attention)![[Pasted image 20240910130833.png]]
- when translating, computes attention weights that determine how much each word should pay attention to the words in the source sentence, new attention weights for each word
- these attention values are calculated in a seperate step for each word with a small neural network![[Pasted image 20240910131705.png]]
- quadratic running time![[Pasted image 20241001051107.png]]
![[Pasted image 20241003032607.png]]