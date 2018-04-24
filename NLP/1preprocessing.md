# Pre-processing text

## Remove punctuation
```py
import string
string.punctuation
def remove_punct(text):
  text_nopunct = "".join[char for char in text if char not in string.punctuation]
  return text_nopunct
```

## Tokenize
Splitting sentence into words
```py
def tokenize(t):
  tokens = re.split('\W+', text)
  return tokens
```

## Lowercase
.lower()
```py
data['body_text_token'] = data['body_text_clean'].apply(lambda x: tokenize(x.lower()))
```

## Remove StopWords
```py
def remove_stopwords(tokenized_list):
  [word for word in tokenized_list if word not in nltk.corpus.stopwords.words('english')]
```

 ## Stemming
 Leave root word, chopping off suffix
 - Problems: Meanness, Meaning -> Mean
 - Explicitly correlates words with similar meanings

 #### PorterStemmer
 ```py
 ps = nltk.PorterStemmer()
 ps.stem('goose') #goos
 ps.stem('geese') #gees
 ```

 ## Lemmatizing
 - Grouping together inflected form of words, basically has goal of stemming
 - Lemmatizing is more accurate as uses more informed analysis, but takes more time
 - If not in wordnet, just leave word

 #### Wordnet lemmatizer
```py
wn = nltk.WordNetLemmatizer()
wn.lemmatize('goose') #goose
wn.lemmatize('geese') #goose
```
