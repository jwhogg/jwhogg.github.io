---
title: 'Word2Vec in detail'
date: 2024-06-02T14:25:04+01:00
draft: true
math: true
katex: true
---

In this article we will introduce the context surrounding word2vec, including the motivation for distributed word embeddings, how the Continious Bag-of-Words and Skip-gram algorithms work, and the advancements since the original paper was released.

| <img src="/images/word2vec_paper_1.png" alt="word2vec paper 1" width="200px" height="150px"> | <img src="/images/word2vec_paper_2.png" alt="word2vec paper 2" width="200px" height="150px"> |
|----------------------------------------------------|-----------------------------------------------------|
| Word2Vec Paper 1- introducing CBOW and Skip-Gram   | Word2Vec Paper 2- Performance Improvements           |

*These 2 papers introduced word2vec to the world back in 2013*

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

The famous example given in the paper is that using vector math with the final embeddings, you could do something like: $\vec{King} - \vec{Man} + \vec{Woman} = \vec{Queen}$. In reality, the resultant vector may not line up exactly with $\vec{Queen}$, but Queen should be the closest vector using [cosine distance](https://medium.com/@milana.shxanukova15/cosine-distance-and-cosine-similarity-a5da0e4d9ded).

see [here](https://www.youtube.com/watch?v=FJtFZwbvkI4) for a great explination from 3b1b on how vectors can encode meaning.

**'Closeness'**: If every word is a vector, 'closeness' between any 2 words (vectors) can be defined as a dot-product of those vectors being close to 1.

**Distributional similarity**- representing a word by means of its neighbors. For a word, its meaning must be encoded by all of the words that are near it in every context. For example, if we look for the word 'banking' across a massive corpus of text, and note all the words nearby, these words must somehow encode the meaning of 'banking'.

### How Word2Vec encodes words
Now we understand why we need to encode words as dense vectors that embed meaning, we can jump in to how word2vec accomplishes this. The paper establishes 2 'fake' tasks that get the model to learn embeddings: ...