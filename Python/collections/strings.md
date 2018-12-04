# Strings

- ' ' and " " are the same
- `chr(ord('a')+1)` to add one to 'a' and get 'b'

## Formatting

Python 3 handles {} others need {0}

```python
`"Hi {} there {}".format(firstP, secondP)`
'{:02d}'.format(i) #print with 2 places

"My quest is {name}"             # References keyword argument 'name'
```



- Returns a single string with {} replaced

## r"..." 
The r doesn't change the type at all, it just changes how the string literal is interpreted. Without the  r, backslashes are treated as escape characters. With the r, backslashes are treated as literal.

## Check proper

```python
'a'.isalpha()
'1'.isdigit()
```

