# Pandas

```python
import pandas as pd

fullCorpus = pd.DataFrame({
  'label': labelList,
  'body_list': textList
})

fullCorpus.head() #print first 5 rows
```
## Read in seperated data
```python
fullCorpus = pd.read_csv("file.tsv", sep="\t", header=None)
# header default  assumes first row is the column names
fullsCorpus.columns = ['label', 'body_text'] # add columns
```

## Create New Column
`pdData['clean_text'] = data['body_text'].apply(lambda x: remove_punct(x))`

## Indexing

Use `X.iloc[0]` instead of `X[0]`

