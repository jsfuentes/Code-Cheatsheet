# Regular Expression
Is case sensitive

[j-q] matches single character between j-1
j+ matches 1+ chars
[j-q0-9]+ matches j9q0
[j-q]+[0-9]+ matchs jq9 not j8q0
```import re```

# Splitting String to List
Re.split('reExpression', string)
OR Re.findall('reExpression', string)
- '\s' #single white space
- '\s+' #split on one or more whitespace
- '\S+' #one or more non whitespace character
- '\w+') #one or more words
- '\W+' #any non word character

# Replace
re.sub('reExpression', "new text")

'\\\\' as the pattern string, because the regular expression must be \\, and each backslash must be expressed as \\ inside a regular Python string literal.

The solution is to use Python’s raw string notation for regular expression patterns; backslashes are not handled in any special way in a string literal prefixed with 'r'