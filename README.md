# simple_chabot_model
A program which takes in user input and generates a text output.

It is composed of 3 main sections:
* A `greetings` function,
* A multiclass classification based `InputModel` class, 
* A data-to-text generation based `OutputModel` class.

The input and output model are used to generate a response to each user input.

### Greetings
Consists of 3 different greetings: 
* `greet_by_joke`, `greet_by_quote`, `greet_by_fact`.

Note that this function is simplified to focus on the general flow of the conversation:
1. takes in user greetings to start conversation
2. outputs simple greetings (e.g 'hi', 'hello', 'hey') (variation: use datetime.datetime object to customize greetings for different times of the day)
3. outptus a joke / quote / fun fact 
4. takes in user response to joke / quote / fun fact
5. performs sentiment analysis and outputs the 😄  emoji for a positive sentiment, 😞  for negative, and 😐  for neutral.

### Input Model
This takes the `BertClassifier` model from the [Tensorflow Model Garden](https://github.com/tensorflow/models/tree/master/official) and trains it on the `Dart` dataset from `tfds-nightly`.

The model takes a word concatenated to its context (a sentence) as input and outputs a vector of logit values for each of the 3 labels: 
`Subject`, `Predicate`, `Object`.

Other functions in the class are used to preprocess the user input into the required format and transform the model outputs to 
an appropriate input for the output model

### Output Model
This takes the [Huggingface](https://huggingface.co/transformers/) `T5ForConditionalGeneration` model and trains it on the `webNLG` dataset from `tfds-nightly`.

The model takes a string of concatenated RDF triples and generates a text based on it.

Other functiosn in the class are used to encode and decode the inputs and outputs of the model.

### References
Dart dataset used in `input_model.py`
```
@article{radev2020dart,
  title={DART: Open-Domain Structured Data Record to Text Generation},
  author={Dragomir Radev and Rui Zhang and Amrit Rau and Abhinand Sivaprasad and Chiachun Hsieh and Nazneen Fatema Rajani and Xiangru Tang and Aadit Vyas and Neha Verma and Pranav Krishna and Yangxiaokang Liu and Nadia Irwanto and Jessica Pan and Faiaz Rahman and Ahmad Zaidi and Murori Mutuma and Yasin Tarabar and Ankit Gupta and Tao Yu and Yi Chern Tan and Xi Victoria Lin and Caiming Xiong and Richard Socher},
  journal={arXiv preprint arXiv:2007.02871},
  year={2020}
```

webNLG dataset used in `output_model.py`
```
@inproceedings{gardent2017creating,
    title = ""Creating Training Corpora for {NLG} Micro-Planners"",
    author = ""Gardent, Claire  and
      Shimorina, Anastasia  and
      Narayan, Shashi  and
      Perez-Beltrachini, Laura"",
    booktitle = ""Proceedings of the 55th Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)"",
    month = jul,
    year = ""2017"",
    address = ""Vancouver, Canada"",
    publisher = ""Association for Computational Linguistics"",
    doi = ""10.18653/v1/P17-1017"",
    pages = ""179--188"",
    url = ""https://www.aclweb.org/anthology/P17-1017.pdf""
}
```
