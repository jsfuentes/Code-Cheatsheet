# Regular Expression
`import re`

# Splitting String to List
Re.split([reExpression], [string])
OR Re.findall([reExpression], [string])
- '\s' #single white space
- '\s+' #split on one or more whitespace
- '\S+' #one or more non whitespace character
- '\w+') #one or more words
- '\W+' #any non word character

# Replace
re.sub('reExpression', "new text")

'\\\\' as the pattern string, because the regular expression must be \\, and each backslash must be expressed as \\ inside a regular Python string literal.

The solution is to use Python’s raw string notation for regular expression patterns; backslashes are not handled in any special way in a string literal prefixed with 'r'