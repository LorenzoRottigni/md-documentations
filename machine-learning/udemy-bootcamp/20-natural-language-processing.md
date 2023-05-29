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

