---
title: 'Word2Vec Overview'
date: 2024-06-02T14:25:04+01:00
draft: false
math: true
katex: true
readingtime: true
---
In this article we will introduce the context surrounding word2vec, including the motivation for distributed word embeddings, how the Continious Bag-of-Words and Skip-gram algorithms work, and the advancements since the original paper was released. We will also go into the training of the neural network, so it is assumed you have some knowledge on this.

| <img src="/images/word2vec_paper_1.png" alt="word2vec paper 1" width="200px" height="150px"> | <img src="/images/word2vec_paper_2.png" alt="word2vec paper 2" width="200px" height="150px"> |
|----------------------------------------------------|-----------------------------------------------------|
| Word2Vec Paper 1- introducing CBOW and Skip-Gram   | Word2Vec Paper 2- Performance Improvements           |
    
<p style="text-align: center; font-size: small; color: gray;">These 2 papers introduced word2vec to the world back in 2013</p>

### Motivation

For many NLP tasks, we need to learn on data which can't be easily represented numerically. For example, let's look at the popular [IMDB dataset](https://huggingface.co/datasets/stanfordnlp/imdb/viewer/plain_text/train), which gives reviews in one column, and a binary sentiment label in the next.
<img src="/images/imdb.png" alt="IMDB dataset"/>
Neural Networks accept vectors, so we need a way to represent these strings as such.

**The 'old' way:** 

We can reprent a corpus of words using a [Bag-of-Words](https://en.wikipedia.org/wiki/Bag-of-words_model). For some input text, we can create an unordered 'bag' of the text's vocabulary (set of unique words), and how many count times it appears in the text.

Raw text:
```
"Ogres are like onions, onions have layers.
```
Bag-of-Words:
```
{"Ogres": 1, "are": 1, "onions": 2, "like": 1, "have": 1, "layers": 1}
```

We can use a BOW to represent any word from our corpus using [one-hot encoding](https://www.geeksforgeeks.org/ml-one-hot-encoding/):

Onions:  <pre>[0,0,1,0,0,0]</pre>

Ogres: <pre>[1,0,0,0,0,0]</pre>

Although an ML model *could* learn using this method, it is grossly inefficient: imagine a corpus with a vocabulary (number of unique words) of 100,000. This would mean you would need a combined vector size of 1,000,000 to encode just 10 words, where 99.9% of the vector is empty.

**The 'new' way**:

word2vec creates a **distributed representation** of words, which is much more efficient, and allows much a much larger corpus of text to be used in training. 

Each vector is continious and dense, where vectors that are closer have similar meanings. This distributed representation of a large text corpus is our goal, so we can use it in other NLP tasks, and word2vec is how we will accomplish it. Since 2013, there are better ways to do this, such as [BERT](https://arxiv.org/abs/1810.04805) and [GloVe](https://nlp.stanford.edu/projects/glove/), which can embed more nuanced relationships between words.

Dense embedding of 'Ogre':
<pre>
array([ 7.10577386e-01, -5.09895974e-01,  1.71235001e+00,  2.05854094e+00, -4.47590043e-01, -1.00782587e+00, -1.14494191e+00, -7.94087996e-01, -2.22047371e-01,...])

array_shape: (400,)
</pre>

The famous example given in the paper is that using vector math with the final embeddings, you could do something like: $\vec{King} - \vec{Man} + \vec{Woman} = \vec{Queen}$. In reality, the resultant vector may not line up exactly with $\vec{Queen}$, but Queen should be the closest vector using [cosine distance](https://medium.com/@milana.shxanukova15/cosine-distance-and-cosine-similarity-a5da0e4d9ded).

see [here](https://www.youtube.com/watch?v=FJtFZwbvkI4) for a great explination from 3b1b on how vectors can encode meaning.

**'Closeness'**: If every word is a vector, 'closeness' between any 2 words (vectors) can be defined as a dot-product of those vectors being close to 1.

**Distributional similarity**- representing a word by means of its neighbors. For a word, its meaning must be encoded by all of the words that are near it in every context. For example, if we look for the word 'banking' across a massive corpus of text, and note all the words nearby, these words must somehow encode the meaning of 'banking'.

## How Word2Vec encodes words
Now we understand why we need to encode words as dense vectors that embed meaning, we can jump in to how word2vec accomplishes this. The paper establishes 2 'fake' tasks that get the model to learn embeddings:

<img src="/images/cbow_skipgram.png" alt="word2vec paper 1" width="80%">

#### Continuous Bag-of-Words (CBOW)
The neural network is passed a few context words from around the target word, with the goal of predicting what that target word is.

#### Skip-gram
The opposite of CBOW, the model is instead passed the middle word, with the goal of predicting the context words around it.

note: **These words will be passed to the model as one-hot encodings**

### Retrieving embeddings
<img src="/images/word2vecnetwork.png" alt="word2vec network" width="80%">
<p style="font-size: small; color: gray;">A matrix-focused view of the model architecture, imagine data flowing left->right</p>
With the above representation of our word2vec model, the matrix $w_{1}$ (representing weights for the input -> hidden layer) **is actually the embeddings table for our words!** This is the 'synthetic task' that we have been training for, where the real goal is actually getting good embedding vectors.

<div style="text-align: center;">
    <img src="/images/hiddenlayeriswordvector.png" alt="word2vec network" width="50%">
    <p style="font-size: small; color: gray;">credit: Chris McCormik</p>
</div>

### Softmax activation
Although later word2vec papers go on to describe the more efficient [hierarchical softmax](https://paperswithcode.com/method/hierarchical-softmax), we will focus just on how softmax helps us clarify which word the network is predicting.

$$  \text{Softmax}(x_{i}) = \frac{\exp(x_i)}{\sum_j \exp(x_j)}  $$

<div style="text-align: center;">
    <img src="/images/softmax.png" alt="softmax demo" width="65%">
    <p style="font-size: small; color: gray;">Where the softmax gets applied (imagine data flow left->right)</p>
</div>

The [softmax activation](https://en.wikipedia.org/wiki/Softmax_function) can take a vector of numbers, and maps each number to between $[0,1]$, where the sum of the vector will always add up to 1. From this, we can find our model's prediction by getting the element with the highest number.

## Training
Using a context window, we can generate pairs for the model in the form: **(TARGET,CONTEXT)**
<div style="text-align: center;">
    <img src="/images/ogresonions1.png" alt="ogres are like onions" width="80%">
    <!-- <p style="font-size: small; color: gray;">Where the softmax gets applied (imagine data flow left->right)</p> -->
</div>
Becomes the following pairs:
<pre>
(onions,ogres), (onions,are), (onions,like), (onions,they), (onions,have), (onions,layers)
</pre>
And using the next target word:
<div style="text-align: center;">
    <img src="/images/onionsogres2.png" alt="ogres are like onions" width="80%">
    <p style="font-size: small; color: gray;">Let's assume our corpus ends at 'layers', otherwise with context = 3 there would be another word on the right</p>
</div>
Becomes these pairs:
<pre>
(they,ogres), (they,are), (they,like), (they,onions), (they,have), (they,layers)
</pre>

Using a training pair, $(Y,X)$ (both one-hot encoded), the model will get passed $X$, and have its output compared against $Y$ to learn from.

#### Distinction between CBOW and Skip-gram training
It's important to make a distinction regarding these pairs for the 2 models, because they *are* slightly different:
* For Skip-gram, the model would be passed a target word ($Y$), and for output, predicts **all** the words within the context window ($ X_{i-n} $). If we had 10 words in the vocabularly, and a context size 3, this would make the model's output vector shape (6,10)- one row for each context word.
* For CBOW, the model is passed all words in the context window ($X_{i-n}$), and for output, predicts the target word that fits the best ($Y$). Inside the neural network, the projection layer, which maps input to the hidden layer, a**verages all the word vectors into one**, so after this step, the network is working with one average word vector.

That's just about it! I hope you've learned something from this article- in the next one in this series, I will be going through building the word2vec CBOW model in python within numpy.

Sources / Further Reading:
* [Chris McCormik- Word2Vec guide](https://mccormickml.com/2016/04/19/word2vec-tutorial-the-skip-gram-model/)

* [Word2Vec from scratch with python and numpy](https://nathanrooy.github.io/posts/2018-03-22/word2vec-from-scratch-with-python-and-numpy/)

* [Jake Tae- Word2Vec from scratch](https://jaketae.github.io/study/word2vec/)

* [Word2Vec original paper](https://arxiv.org/abs/1301.3781)