## Image Captioning Model based on Attention

To understand the context of an image and explain it in a natural language like English, an image caption generator uses computer vision and natural language
processing techniques. We have constructed the caption generator using CNN and LSTM in this Python-based project.

We used Flickr8k dataset which contains around 8000 images with 5 captions each.

### Attention
Attention is used to boost the ability of the network to predict better captions. The Attention module helps the model to focus on the most relevant part of the image for generating the word.


### Preprocessing
Firstly, we used a pre-trained CNN-based network Inception that takes in raw images as input and produces encoded image vectors that capture the essential features of the image. 
We used a pre-trained Inception model which consists of two sections:
The first section consists of a sequence of CNN layers that progressively extract the relevant features from the image to produce a compact feature map representation.
The second section is the Classifier that consists of a sequence of Linear layers. It takes the image feature map and predicts a class (eg. dog, car, house, etc) to which the feature belongs.

We downloaded the Inception model and use only the first section which produces the image feature vectors.

We also preprocessed the captions by performing the following steps: converting to lowercase, removing punctuation, removing 1 character words, converting words to word IDs and padding all captions to the same length. 

Thus, our training data consists of:
1. features (X) - the encoded feature vectors
2. target labels (y) - the captions

### Model

Encoder: since the image encoding has already been done by the pre-trained Inception model, the Encoder here is very simple. It consists of a Linear layer that takes the pre-encoded image features and passes them on to the Decoder.

Sequence Decoder: this is a recurrent network built with GRUs. The captions are passed in as the input after first going through an Embedding layer.

Attention: as the Decoder generates each word of the output sequence, the Attention module helps it to focus on the most relevant part of the image for generating that word.

Sentence Generator: this module consists of a couple of Linear layers. It takes the output from the Decoder and produces a probability for each word from the vocabulary, for each position in the predicted sequence.
