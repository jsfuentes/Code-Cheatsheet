# Pandas

```python
import pandas as pd

fullCorpus = pd.DataFrame({
  'label': labelList,
  'body_list': textList
})

fullCorpus.head() #print first 5 rows
```
## Access

```python
df['date'] #just date column 
df[df['date'] > '2017-03-20'] # just date columns that meet criteria
```

### Filter

```python
df = df.drop(['high','low','close','volume'], axis=1) #get rid of columns 
```

### Indexing

Use `X.iloc[0]` instead of `X[0]`

## Read in seperated data

```python
fullCorpus = pd.read_csv("file.tsv", sep="\t", header=None)
# header default assumes first row is the column names
fullsCorpus.columns = ['label', 'body_text'] # add columns
```

## Create New Column
`pdData['clean_text'] = data['body_text'].apply(lambda x: remove_punct(x))`