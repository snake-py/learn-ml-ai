# NLP

Three steps to NLP:

- preprocessing
- modeling (preprocessing + training)
- postprocessing    

# Preprocessing or called normalization 

- remove punctuation and upper/lower case
- tokenization (assign a unique id to each word)
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