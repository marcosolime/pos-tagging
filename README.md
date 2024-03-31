# Assignment 1 - POS tagging

![POS tagging](/img/pos_tagging.png)

## Task description
Part-of-Speech (POS) tagging is an NLP task that involves assigning a grammatical category (part of speech) to each word in a sentence. These categories include nouns, verbs, adjectives, adverbs, pronouns, etc.

## Workflow
In this task we train a custom model on a labelled dataset. This dataset consists of a set of documents, where each word has its POS label associated. We train our model on a subset of this dataset, and test it on another subset.

After downloading the corpus (![Penn Treebank](https://www.ling.upenn.edu/courses/Fall_2003/ling001/penn_treebank_pos.html)), we create a vocabulary of words leveraging ![GloVe embeddings](https://nlp.stanford.edu/projects/glove/). We use such vocabulary to tokenize our dataset and as a lookup table (or embedding matrix) in the Embedding layer of our neural model.

We try 3 different models. All of them are include recurrent neural networks.
- Baseline: Embedding layer, Bidirectional LSTM, Dense layer
- Model 1: similar to the baseline, but with 2 LSTMs instead of 1
- Model 2: similar to the baseline, but with 2 dense layers

All of the models are comperable in term of parameters (20 millions).

The embedding layers are pre-initialized with GloVe embeddings and kept frozen during training.

We train our model using categorical crossentropy loss and optmizing with Adam (lr=0.001). We also plot the macro f1 score, precision and recall during training.

![Metrics train set](/img/metrics_train.png)

During evaluation, we calculate the f1 score and other metrics for each label individually on the test set.

![F1 test](/img/f1_test.png)

Interestingly, we notice that rare labels - tags that appear very rarely on the train set - have zero score both on precision and recall. We conjecture that since such labels are so few in the train set, the model struggles a lot to learn them, and as a consequence it scores very poorly on the validation.

## Licence
MIT license