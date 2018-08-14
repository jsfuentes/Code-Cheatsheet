## Strings
- '' and "" are the same
- `chr(ord('a')+1)` to add one to 'a' and get 'b'

## Formatting
`"Hi {} there {}".format(firstP, secondP)`
- Returns a single string with {} replaced

## r"..." 
The r doesn't change the type at all, it just changes how the string literal is interpreted. Without the  r, backslashes are treated as escape characters. With the r, backslashes are treated as literal.

## Check proper

```python
'a'.isalpha()
'1'.isdigit()
```

