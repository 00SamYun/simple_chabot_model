# input_model
This talks about the result from some research and experimenting with the input model.

### A little about BERT
BERT is a transformer based model which reads an input sequence in its entirety - thus 'bidirectional' - 
as opposed to most other language models which is tasked with predicting the next word in a sequence.
The BERT model is pretrained on 2 learning tasks: Masked LM (MLM) and Next Sentence Prediction (NSP).
These allow the model to better understand the context of each words. 

In this project, the model is required to predict the role of a word (subject, predicate, object) which is 
dependent on both its part of speech and its position in a sentence. Thus the BERT model is the most appropriate.

### Loss, Metrics and Optimizers
##### Loss
The most commonly used loss function in multiclass classification is [Cross entropy](https://en.wikipedia.org/wiki/Cross_entropy).
Tensorflow keras provides 2 variations of this loss function: `CategoricalCrossentropy` and `SparseCategoricalCrossentropy`. 

Since our task only involves 3 labels, the tf.keras.losses.CategoricalCrossentropy(from_logits=True) loss function is used. 

##### Metrics
Metrics used for multiclass classification are narrowed down to the following 3:
* categorical_accuracy: mean accuracy rate across all predictions
* sparse_categorical_accuracy: categorical_accuracy for a large number of classes (target value is a large matrix populated by almost all zeros)
* top_k_categorical_accuracy: checks if the correct class is in one of the top k predictions

This model uses tf.keras.metrics.CategoricalAccuracy() to match with the loss function.

##### Optimizers
The most common optimizers are [SGD (stochastic gradient descent)](https://en.wikipedia.org/wiki/Stochastic_gradient_descent) and Adam 
([adaptive learning rate method](https://wiki.tum.de/display/lfdv/Adaptive+Learning+Rate+Method)).

This model was trained on both `tf.keras.optimizers.Adam()` and `tf.keras.optimizers.SGD()`, with the latter producing better results.

*Accuracy of Adam optimizer after 3 epochs was 41.72% whereas Accuracy of SGD optimizer was 95.25%.*

### Hyperparameters 
`BATCH_SIZE_PER_REPLICA` was set to 32 after experimenting with 16, 64 and a combination of all three. 
Setting it to 128 and 256 caused a `ResourceExhausted` error.

`EPOCHS` was set to 8 after monitoring the val loss for 10 epochs.

The `learning_rate` parameter for the SGD optimizer is set to the default (0.01).
This value is obtained using the [lr_finder](https://github.com/avanwyk/tensorflow-projects/tree/master/lr-finder) 
linked in [this](https://www.avanwyk.com/finding-a-learning-rate-in-tensorflow-2/) blog.
