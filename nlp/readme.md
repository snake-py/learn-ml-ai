# NLP

Three steps to NLP:

- preprocessing
- modeling (preprocessing + training)
- postprocessing

# Preprocessing or called normalization

- remove punctuation and upper/lower case
- tokenization (assign a unique id to each word) // often not considered a text preprocessing, because it is not changing the text - it is rather transforming it into a list of tokens or word
- stemming (bluntly remove suffixes, like -ing, -ly, -ed, -s and)
- lemmatization (substitute each word by its root, e.g. 'is' by 'be' or went by 'go')
- stopword removal (remove stopwords, like and, the, a, is, etc.)

## Stop Words

```python
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
stop_words = set(stopwords.words('english'))

some_text = "This is a sample sentence, showing off the stop words filtration."
tokenized_text = word_tokenize(some_text)
text_no_stops = [word for word in tokenized_text if word not in stop_words]

# Output
"""
['This', 'sample', 'sentence', ',', 'showing', 'stop', 'words', 'filtration', '.']
"""
```

## Stemming

<br>

```python
from nltk.tokenize import word_tokenize
from nltk.stem import PorterStemmer
stemmer = PorterStemmer()

some_text = "This is a sample sentence, showing off the stop words filtration."
tokenized_text = word_tokenize(some_text)
stemmed = [stemmer.stem(word) for word in tokenized_text]

# Output
"""
['thi', 'is', 'a', 'sampl', 'sentenc', ',', 'show', 'off', 'the', 'stop', 'word', 'filtrat', '.']
"""

```

## Lemmatization

```python
from nltk.tokenize import word_tokenize
from nltk.stem import WordNetLemmatizer
lemmatizer = WordNetLemmatizer()

some_text = "This is a sample sentence, showing off the stop words filtration."
tokenized_text = word_tokenize(some_text)
stemmed = [lemmatizer.lemmatize(word) for word in tokenized_text]

# Output
"""
['This', 'is', 'a', 'sample', 'sentence', ',', 'showing', 'off', 'the', 'stop', 'word', 'filtration', '.']
"""

```

<hr>

<br>

# Part-of-Speech Tagging

Definition:

This process is grouping words and phrases into a specific part of speech. Means here we look for the meaning of the word and phrases.

- look for synonyms (wordnet is a database of synonyms)
- use synonyms to find the meaning of the word (determine the part of speech)
- return the most common part of speech

In practice, it is as simple as passing a get_part_of_speech() function to the lemmatizer.

```python
from nltk.tokenize import word_tokenize
from nltk.stem import WordNetLemmatizer
from part_of_speech import get_part_of_speech

def get_part_of_speech(word):
  probable_part_of_speech = wordnet.synsets(word)

  pos_counts = Counter()

  pos_counts["n"] = len(  [ item for item in probable_part_of_speech if item.pos()=="n"]  )
  pos_counts["v"] = len(  [ item for item in probable_part_of_speech if item.pos()=="v"]  )
  pos_counts["a"] = len(  [ item for item in probable_part_of_speech if item.pos()=="a"]  )
  pos_counts["r"] = len(  [ item for item in probable_part_of_speech if item.pos()=="r"]  )

  most_likely_part_of_speech = pos_counts.most_common(1)[0][0]

  return most_likely_part_of_speech


lemmatizer = WordNetLemmatizer()

some_text = "This is a sample sentence, showing off the stop words filtration."
tokenized_text = word_tokenize(some_text)
stemmed = [lemmatizer.lemmatize(word, get_part_of_speech(word)) for word in tokenized_text]
```

# Example of preprocessing

```python
from nltk.tokenize import word_tokenize, sent_tokenize
from nltk.stem import WordNetLemmatizer
from part_of_speech import get_part_of_speech
import re

lemmatizer = WordNetLemmatizer()

input_text = '<p>A cryptocurrency is a digital or virtual currency that is secured by cryptography, which makes it nearly impossible to counterfeit or double-spend. Many cryptocurrencies are decentralized networks based on blockchain technology.</p>'

inner_paragraph = re.sub('<.?p>', '', input_text)
removed_periods = re.sub('\.', '', inner_paragraph)
text_lower = removed_periods.lower()

tokenized = word_tokenize(text_lower)
lemmatized = [lemmatizer.lemmatize(word, get_part_of_speech(word)) for word in tokenized]

print(tokenized)
```

<br>

# NLP Models

- bag of words (bow)

## Bag of Words (BoW)

common use cases:

- topic determination in songs
- filtering spam emails
- sentiment analysis (positive/negative, e.g. if a tweet is negative or positive)
- classification of news articles
- creating word clouds

<br>

BoW is only concerned about word counts, not the meaning of the words. Therefore it can calculate ngrams or single words (unigram).

```python
## Bag of Words probably easier to achieve using a counter object
def text_to_bow(some_text):
  bow_dictionary = {}
  tokens = preprocess_text(some_text)
  for token in tokens:
    if token in bow_dictionary :
      bow_dictionary[token] = bow_dictionary[token] + 1
    else:
      bow_dictionary[token] = 1
  return bow_dictionary
```

## Bow Vectors

Is used for topic modeling and text classification. Therefore feature vectors are calculated and compared.

A feature vector is a numeric representation of a combination of features. For instance, if we want to find the similarity between two documents, we can preset features for which we are looking for.

A feature could be: is_review, is_long, has_ratings, is_talking_about_topic_a, is_talking_about_topic_b

With this we can create a feature vector - following the table view of the feature vector.

| article   | is_review | is_long | has_ratings | is_talking_about_topic_a | is_talking_about_topic_b |
| --------- | --------- | ------- | ----------- | ------------------------ | ------------------------ |
| article 1 | 1         | 0       | 0           | 1                        | 0                        |
| article 2 | 1         | 0       | 0           | 0                        | 1                        |
| article 3 | 1         | 1       | 1           | 1                        | 1                        |

With these vectors we can calculate the similarity between two documents, by calculate the distance.

But how to determine if the feature is included in the text?

This is known a s feature extraction or vectorization process. Therefore all the words of a text are counted and then it is checked if the condition is met toi assign a feature value.

codecademy is showing this feature extraction process 
```python
def create_features_dictionary(documents):
  features_dictionary  = {}
  merged = ' '.join(documents)
  tokens = preprocess_text(merged)
  index = 0
  for token in tokens:
    if token not in features_dictionary:
      features_dictionary[token] = index
      index += 1
  return features_dictionary, tokens


training_documents = ["Five fantastic fish flew off to find faraway functions.", "Maybe find another five fantastic fish?", "Find my fish with a function please!"]

print(create_features_dictionary(training_documents)[0])
```

