# 20 Natural Language Processing

NLP provides several tools to process human language. It is used to analyze text, allowing machines to understand how human speak. It is used in chatbots, spam filters, and grammar checkers.
In order to work with natural language it's necessary to follow these steps:

- Compile Documents: The first step is to compile the documents that will be used to train the model. This step is also known as corpus.
- Featurize Documents: The second step is to extract features from text. This step is also known as vectorization.
- Compare Features: The third step is to compare the features of the documents. This step is also known as similarity.

## Bag of Words
NLP transforms text into a more understandable format for machines:

Documents "Blue House" and "Red House" gets transformed into vectors:
"Blue House" => (red,blue,house) => (0,1,1)
"Red House" => (red,blue,house) => (1,0,1)

A document represented as a vector of word is called a bag of words.
In order to determine the similarity between two documents, we can use the cosine similarity:

cosine similarity = sim(A,B) = cos(0) = (A*B) / (||A||*||B||)

It's possible to improve the bag of words by adjusting the words count based on their frequency in the corpus. This is called term frequency-inverse document frequency (TF-IDF).

## Terminology

- Corpus: A collection of documents.
- Stop Words: Common words that are unlikely to be useful for learning, such as "and", "the", "a", etc.
- Token: A single element of a corpus, such as a word or a symbol.
- Tokenization: The process of splitting a document into tokens.
- Vector: A list of numbers that represent a document.
- Vectorization: The process of converting a document into a vector.
- Cosine Similarity: A measure of similarity between two vectors.
- Bag of Words: A vector representation of a document that describes the occurrence of words within a corpus.

## TF-IDF
It's a measure of the frequency of a word in a document, adjusted for the frequency of the word in the corpus.
It's mathematically expressed as:

W(i,j) = TF(i,j) * log(N/DF(i))

Where:
- W(i,j) is the weight of the word i in the document j.
- TF(i,j) is the frequency of the word i in the document j.
- N is the number of documents in the corpus.
- DF(i) is the number of documents in the corpus that contain the word i.

### Term frequency
Importance of the term within the document. TF(d,t) = Number of occurences of term t in document d.
### Inverse term frequency
Importance of the term in the corpus.


## Python Implementation
Python has a library called "nltk" that provides several tools to work with natural language.

```
conda install nltk
pip3 install nltk
```

```
import matplotlib.pyplot as plt
import seaborn as sns
import nltk
%matplotlib inline
```

nltk provides an interface to download several corpora and models. The following command will open a shell to download the corpora and models:

```
nltk.download_shell()
```

### Dataframe
```
messages = pd.read_csv('SMSSpamCollection', sep='\t', names=['label', 'message'])
messages.head()
```

ham messages count vs spam messages count:
```
messages.groupby('label').describe()
```

An important part of NLP is about feature engineering, several features might be extracted from text data, such as:
- length of the text
- number of words
- number of characters
- number of punctuations
- number of upper case words
- number of title case words
- number of stop words
- number of special characters
- number of numerics
- number of emojis
- number of hashtags
- number of mentions
- average length of the words
- average length of the sentences
- number of sentences
- number of unique words
- number of unique words without stopwords
- number of words with only alphabets

```
messages['length'] = messages['message'].apply(len)
```

### Plotting
Disribution of messages length:
```
messages['length'].plot.hist(bins=150)
```

Finding a message with 910 characters:
```
messages[messages['length'] == 910]['message'].iloc[0]
```

Plotting the distribution of the length of the messages by label:
```
messages.hist(column='length', by='label', bins=60, figsize=(12, 4))
```

It's possible to see that spam messages tend to have more characters

### Text Preprocessing
The following steps are necessary to process text data:
- Remove punctuation
- Remove stopwords
- Tokenize
- Lemmatize or Stem

```
import string

def text_process(mess):
    """
    1. remove punctuation
    2. remove stopwords
    3. return list of clean text words
    """
    nopunc = [char for char in mess if char not in string.punctuation]
    nopunc = ''.join(nopunc)
    return [word for word in nopunc.split() if word.lower() not in stopwords.words('english')]
```

### Vectorization
Vectorization is the process of converting text data into vectors. The following steps are necessary to vectorize text data:
- Count how many times a word occurs in each message (known as term frequency)
- Weigh the counts, so that frequent tokens get lower weight (inverse document frequency)
- Normalize the vectors to unit length, to abstract from the original text length (L2 norm)

```
from sklearn.feature_extraction.text import CountVectorizer

bow_transformer = CountVectorizer(analyzer=text_process).fit(messages['message'])
```
how many words are in the vocabulary:
```
print(len(bow_transformer.vocabulary_))
```

```
message4 = messages['message'][3]
# 'U dun say so early hor... U c already then say...'
```

```
bow4 = bow_transformer.transform([message4])
print(bow4)
print(bow4.shape)

# (0, 4068)	2
# (0, 4629)	1
# (0, 5261)	1
# (0, 6204)	1
# (0, 6222)	1
# (0, 7186)	1
# (0, 9554)	2
# -----------
# (1, 11425)
```

Get back the word at index 4068:
```
bow_transformer.get_feature_names_out()[
    # check the word at index 4068
    4068
]
# feature 4068 is 'U' and it appears twice in the message
```
Transform the entire dataframe:
```
messages_bow = bow_transformer.transform(messages['message'])
```

Sparse matrix is a matrix in which most of the elements are zero. In the interest of efficient storage, a sparse matrix will be stored by only storing the locations of the non-zero elements.
It's useful because most of the cells in the matrix are empty, so it's a waste of memory to store all the zeros.
```
print('Shape of Sparse Matrix: ', messages_bow.shape)
print('Amount of Non-Zero occurences: ', messages_bow.nnz)
```
Sparsity is useful to know how many zeros are in the matrix:
```
sparsity = (100.0 * messages_bow.nnz / (messages_bow.shape[0] * messages_bow.shape[1]))
print('sparsity: {}'.format(round(sparsity)))
```

### TF-IDF
TD-IDF stands for Term Frequency - Inverse Document Frequency. It's a numerical statistic that is intended to reflect how important a word is to a document in a collection or corpus.
The TF-IDF tramsformer will calculate the TF-IDF score for each word in the corpus.

```
from sklearn.feature_extraction.text import TfidfTransformer

tfidf_transformer = TfidfTransformer().fit(messages_bow)
```
Transform the message 4:
```
tfidf4 = tfidf_transformer.transform(bow4)

print(tfidf4)
#  (0, 4068)	0.26863320404807484
#  (0, 4629)	0.2283418270966581
#  (0, 5261)	0.2848160159387552
#  (0, 6204)	0.2891210261089915
#  (0, 6222)	0.3273399941961877
#  (0, 7186)	0.6208395209546331
#  (0, 9554)	0.4673241898596147
```
Understanding the importance of word 'university' in the message 4:
```
print(tfidf_transformer.idf_[bow_transformer.vocabulary_['university']])
```
Transform the entire bag-of-words corpus into TF-IDF corpus:
```
messages_tfidf = tfidf_transformer.transform(messages_bow)
```

### Training a model
It's now possible to train a model to classify a message as spam or not spam using for example MultinomialNB classifier.
```
from sklearn.naive_bayes import MultinomialNB

spam_detect_model = MultinomialNB().fit(messages_tfidf, messages['label'])
```
Checking the prediction for the message 4:
```
print('predicted:', spam_detect_model.predict(tfidf4)[0])
# ham
print('expected:', messages.label[3])
# ham
```

### Model Evaluation
Applying the model to all the messages:
```
all_predictions = spam_detect_model.predict(messages_tfidf)
print(all_predictions)
```

```
from sklearn.metrics import classification_report

print(classification_report(messages['label'], all_predictions))
```

```
from sklearn.model_selection import train_test_split

msg_train, msg_test, label_train, label_test = train_test_split(messages['message'], messages['label'], test_size=0.3)
```

## Creating a Data Pipeline
Scikit-learn pipelines are very useful for simplifying the workflow. It's possible to set up all the transformations that we will do to the data for future use.

```
from sklearn.pipeline import Pipeline

pipeline = Pipeline([
    # 1st step => use CountVectorizer to convert text messages into a matrix of token counts
    ('bow', CountVectorizer(analyzer=text_process)),
    # 2nd step => use TfidfTransformer to compute the IDF values and compute the TF-IDF scores
    ('tfidf', TfidfTransformer()),
    # 3rd step => use MultinomialNB classifier to train the model
    ('classifier', MultinomialNB())
])
```
Fit pipeline to the training data:
```
pipeline.fit(msg_train, label_train)
```
Predict the test data:
```
predictions = pipeline.predict(msg_test)
```
Evaluate the model:
```
print(classification_report(predictions, label_test))
```

### Other models
```
from sklearn.ensemble import RandomForestClassifier

pipeline = Pipeline([
    ('bow', CountVectorizer(analyzer=text_process)),
    ('tfidf', TfidfTransformer()),
    ('classifier', RandomForestClassifier())
])

pipeline.fit(msg_train, label_train)

predictions = pipeline.predict(msg_test)

print(classification_report(predictions, label_test))
```

```
from sklearn.svm import SVC

pipeline = Pipeline([
    ('bow', CountVectorizer(analyzer=text_process)),
    ('tfidf', TfidfTransformer()),
    ('classifier', SVC())
])

pipeline.fit(msg_train, label_train)

predictions = pipeline.predict(msg_test)

print(classification_report(predictions, label_test))
```

```
from sklearn.linear_model import LogisticRegression

pipeline = Pipeline([
    ('bow', CountVectorizer(analyzer=text_process)),
    ('tfidf', TfidfTransformer()),
    ('classifier', LogisticRegression())
])

pipeline.fit(msg_train, label_train)

predictions = pipeline.predict(msg_test)

print(classification_report(predictions, label_test))
```