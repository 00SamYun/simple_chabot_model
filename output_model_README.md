# output_model
This talks about the result from some research and experimenting with the output model.

### A little about T5 Transformers
The T5 model is pretrained on 3 different tasks: language modeling, corrupting spans and deshuffling. 
It has an encoder-decoder [seq2seq](https://en.wikipedia.org/wiki/Seq2seq) architecture: 
* encoder trained with a fully visible attention mask (i.e all tokens contribute to the attention of each token)
* decoder trained with a causal mask (i.e each token is affected by every token which comes before it)

T5 transformers come in 3 main sizes - small, base and large. The `t5-large` produces the best results however has a lot more variables to train
and thus this model uses the `t5-base` architecture.

### Loss, Metrics and Optimizers
##### Loss
The `TFT5ForConditionalGeneration` model uses an object of the `transformers.modeling_tf_utils.TFCausalLanguageModelingLoss` class as its loss function
(suitable for predicting the next token of a sequence).

##### Metrics
The metrics used in this model is `tf.keras.metrics.SparseCategoricalAccuracy()` which is suitable for multiclass classification of up to many labels. 
It is most used for prediction of a token from a vocabulary (i.e. text generation).

##### Optimizers
`tf.keras.optimizers.Adam()` is the best optimizer for prediction involving large sparse matrices. 
The default values for the parameters are kept as they yield a good accuracy of 92.53%.

### Hyperparameters
`BUFFER_SIZE` was set to a tenth of the dataset (1812). A larger buffer size produces better results as the dataset is shuffled more thoroughly
but also increases computational memory.

`BATCH_SIZE_PER_REPLICA` is set to 16 - a larger batch size causes a `ResourceExhausted` error. 

`EPOCHS` was set to 5 after monitoring the val loss for 10 epochs.
