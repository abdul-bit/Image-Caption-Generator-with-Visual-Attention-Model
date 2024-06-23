
# Image Caption Generator with Visual Attention Model


**_Abstract -_** Caption generation does not only include
detecting an object in the image but also describes the
interaction between various objects present in the images
and their respective actions.
In this paper, we will be discussing the various models
available in order to generate captions on images and also
describe about the architecture we have implemented
which basically contains an Encoder and Decoder model
along with Visual Attention models to generate
captions.The validation of the captions is performed on a
dataset which is a combination of Flickr 8k and COCO
images.


## Authors

- [Abdul Rahman Shigihalli](https://www.github.com/abdul-bit)
- [Abhishek D](https://github.com/abhishekd23)
- [Pratham S Goleccha](https://www.linkedin.com/in/psg0701)



## Proposed Evaluations

The major challenge that arises in the image captioning
models is that the model must be powerful enough to solve the
challenges arising in the field of computer vision, like
determining which objects are in an image, but they must also
be able to capture and demonstrate their relationships in a
decoded natural language. It is a big challege for machine
learning models to percieve things the way we humans do and
being able to exactly capure all the spatial level and object
level feature dependencies.
In this paper, we design approaches to caption generation that
attempt to incorporate a form of attention inspired from The
work of Neural machine translation in recent paper by
Dzmitry, Cho, Kyunghyun, and Bengio, Yoshua using the
Bahanadou’s attention model.



## Dataset

For Dataset we have prepared our own which is the
combination of Flickr8k and COCO-MS which has a total of
98967 images which approximately 5 captions per image.

## Training details

- _Image Caption Generation Using Resnet-101 Feature Extraction Model and LSTM-based decoder_:

The model leverages exemplar images to map captions
related to captured features and dependencies.

### Feature Extraction

For feature extraction **Encoder**, we use the ResNet-based feature
extraction convolutional neural network.

**ResNet-101** is a convolutional neural network that is 101 layers
deep. For the training purpose, we use a pre-trained version of
the network trained on more than a million images from the
ImageNet database. The pretrained network can easily classify
various images upto 1000 object categories. As a result, the
network has learned rich feature representations for a wide
range of images.

ResNet101 Architeture

In our ResNet101 feature extraction model, we set the last layer
as a hidden layer and the generated feature is of dimension
(100, 2048)
For the Encoder, Our model takes a single raw image and
generates a caption y encoded as a sequence of 1-of-K encoded
words.

In order to obtain a correspondence between the feature vectors
and portions of the 2-D image, we extract features from a lower
convolutional layer, unlike previous work which instead used a
fully connected layer. This allows the decoder to selectively
focus on certain parts of an image by selecting a subset of all
the feature vectors.


For the **Decoder**,
We use a long short-term memory (LSTM) network that
produces a caption by generating one word at every time step
conditioned on a context vector, the previous hidden state and
the previously generated words.
In simple terms, the context vector zˆt is a dynamic
representation of the relevant part of the image input at time t.
We define a mechanism φ that computes zˆt from the annotation
vectors ai , i = 1, . . . , L, corresponding to the features extracted
at different image locations. For each location i, the mechanism
generates a positive weight αi which can be interpreted either as
the probability that location i is the right place to focus for
producing the next word or as the relative importance to give to
location i in blending the ai’s together. The weight αi of each
annotation vector ai is computed by an attention model fatt for
which we use a multilayer perceptron conditioned on the
previous hidden state st−1. 

![image](https://github.com/abdul-bit/Image-Caption-Generator-with-Visual-Attention-Model/assets/59999587/7039689f-d4ce-4f08-97f3-c59683d65fbf)

### Bahanadou’s Attention Model
For the **Attention model**, We represent
the global attention model which is the Bahdanau attention
model inspired from neural machine translation. 

We modelled an overall global attention mechanism inspired
from Neural machine translation in recent paper by Dzmitry,
Cho, Kyunghyun, and Bengio, Yoshua namely Bahdanau
attention. 

The decoder takes the encoder features and passes it
to the attention model together with the previous hidden
decoder state, st−1
This generates an attention score:

![image](https://github.com/abdul-bit/Image-Caption-Generator-with-Visual-Attention-Model/assets/59999587/1ddad6f8-589a-4816-8f1b-cc142750b01d)

The weights are calculated using two dense layers of size 512 ,
one for the hidden state st−1 and the other for the encoded
features.

![image](https://github.com/abdul-bit/Image-Caption-Generator-with-Visual-Attention-Model/assets/59999587/07e82288-dbda-4269-bc09-eb8cae979429)

Here,
V is a weight vector which is a one-dimensional dense layer.
The model is parametrized as a feedforward neural network and
jointly trained with the remaining system components.
Subsequently, a softmax function is applied to each attention
score to obtain the corresponding weight value:

![image](https://github.com/abdul-bit/Image-Caption-Generator-with-Visual-Attention-Model/assets/59999587/adbe5613-c4a2-4485-bfba-95b2871a9067)

The application of the softmax function essentially normalizes
the annotation values to a range between 0 and 1 and, hence, the
resulting weights can be considered as probability values.


## Experimental Results

![image](https://github.com/abdul-bit/Image-Caption-Generator-with-Visual-Attention-Model/assets/59999587/745dee4b-0cfd-490e-862b-cf67aa42e9a3)
![image](https://github.com/abdul-bit/Image-Caption-Generator-with-Visual-Attention-Model/assets/59999587/3eba5300-3b1c-421b-ac30-8c4c1a59a361)
![image](https://github.com/abdul-bit/Image-Caption-Generator-with-Visual-Attention-Model/assets/59999587/6cd19864-3066-4a2c-b9bc-0b24ed4bb151)
![image](https://github.com/abdul-bit/Image-Caption-Generator-with-Visual-Attention-Model/assets/59999587/8a763539-82ef-41db-86b0-1e7c5b58b233)
![image](https://github.com/abdul-bit/Image-Caption-Generator-with-Visual-Attention-Model/assets/59999587/b07d47b8-227a-4fe9-9b62-5906eabf8294)
![image](https://github.com/abdul-bit/Image-Caption-Generator-with-Visual-Attention-Model/assets/59999587/5d573305-c2b1-4fdc-a2c7-523dbfa6ae37)
![image](https://github.com/abdul-bit/Image-Caption-Generator-with-Visual-Attention-Model/assets/59999587/fa557696-225c-494e-a6d6-aff3015cc408)



## References

- **Haoran Wang , Yue Zhang, and Xiaosheng Yu**
 _“An Overview of Image Caption Generation Methods”,_ Research Article Published 8 January 2020.
- **Kelvin Xu, Jimmy Lei Ba†,Ryan Kiros**
 _“**Show, Attend and Tell :** Neural Image Caption Generation with Visual Attention"_
