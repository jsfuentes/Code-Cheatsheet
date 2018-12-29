# Strings

- ' ' and " " are the same
- `chr(ord('a')+1)` to add one to 'a' and get 'b'
- Python 3 has strings be unicode, 2 byte character

## Formatting

Python 3 handles {} others need {0}

```python
`"Hi {} there {}".format(firstP, secondP)`
'{:02d}'.format(i) #print with 2 places

"My quest is {name}".format(name="jorge")             # References keyword argument 'name'
```

- Returns a single string with {} replaced

## r"..." = raw
still string, but treats backslashes as literals instead of escape characters

### u"...." = Unicode

## Check proper

```python
'a'.isalpha()
'1'.isdigit()
```

## Get lists

```
string.ascii_uppercase
```