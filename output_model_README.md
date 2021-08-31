# output_model
This talks about the result from some research and experimenting with the output model.

### A little about T5 Transformers
The T5 model is pretrained on 3 different tasks: language modeling, corrupting spans and deshuffling. 
It has an encoder-decoder [seq2seq](https://en.wikipedia.org/wiki/Seq2seq) architecture: 
* encoder trained with a fully visible attention mask (i.e all tokens contribute to the attention of each token)
* decoder trained with a causal mask (i.e each token is affected by every token which comes before it)

These make the T5 model a good for text generation.

### Loss, Metrics and Optimizers

### Hyperparameters
