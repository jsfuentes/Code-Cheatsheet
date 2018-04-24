# Vectorizing
Encoded text as integer to create feature vector

Hyper parameters: N-grams(uni-bigrams, just bigrams, uni-bi-trigrams)

## Overview
Each Column is the word/element and each Row is the document, each element is the count

## Count Vectorizer
Since mostly zeros, Sparse Matrix, only stores non zero elements.
```py
from sklearn.feature_extraction.text import CountVectorizer
def clean_text(text):
  ....
count_vect = CountVectorizer(analyzer=clean_text)
X_counts = count_vect.fit_transform(data) #fit would just learn, fit transform returns
```

#### Analysis
```py
X_counts.shape
count_vect.get_feature_names()
X_counts_df.columns = pd.DataFrame(X_counts.toarray()) #X_counts is sparse rn
X_counts_df.columns = count_vect.get_feature_names()
```

## N-grams
Same a count vectorizer, but now columns represent all combinations of adjacent words of length n in your text
- nlp is an interesting
  - => nlp is, is an, an interesting
  - => nlp is an, is an interesting,
- Wants a string passed into it, not a list

```py
CountVectorizer(ngram_range=(1,2)) #unigrams and bigrams
CountVectorizer(ngram_range=(1,3)) #unigrams and bigrams and trigrams
CountVectorizer(ngram_range=(2,2)) #bigrams
#see above for training/analysis
```

## Term Frequency Inverse Document Frequency TF-IDF
- Cells represent a weighting to how important that word is to the document taking into account rarity and size of doc
- cell = word in doc / total # of doc * log(total doc #/# of docs with i)
```py
from sklearn.feature_extraction.text import
tf = TfidfVectorizer()
X = tf.fit_transform(data)
```
