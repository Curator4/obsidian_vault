- generatively pretrained transformer
- combines use of attention (rnn) and cnn (convolutions) optimizations
### self-attention
- essentially, computes an attention representation for each word, compared to every other word. uses the values q, K, V, each of which has its own weights 
- each word has a accompanying q, k and v value which is used to determine the attention![[Pasted image 20241024125955.png]]
### multi-head attention
- basically just a big for-loop over the self attention mechanism, but can be computed in parallel
- each head can intuitively represent a different feature like, who, where, when
- $h = \#heads$ ![[Pasted image 20241024133330.png]]

### transformer network
- the core idea is to have a attention model that can be computed in parallel
- structured consists of a encoder block that runs n times, and an encoder block ![[Pasted image 20241024140958.png]]
- also uses position encoding 
- ![[Pasted image 20241120173009.png]]
- ![[Pasted image 20241120213709.png]]
- ![[Pasted image 20241120213938.png]]
- ![[Pasted image 20241120214257.png]]