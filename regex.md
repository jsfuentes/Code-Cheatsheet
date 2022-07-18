# Regular Expression

https://regexr.com/

Is case sensitive

[j-q] matches single character between j-q
j+ matches one or more j's
[j-q0-9]+ matches j9q0
[j-q]+[0-9]+ matches jq9 not j9q0

| Symbol | Effect             | Example            |
| ------ | ------------------ | ------------------ |
| .      | any char           | a.b => aye         |
| *      | 0-any of last char | ba* => baaaaa & b  |
| +      | 1-any of last char | ba+ => baaaaa & ba |
| ^      | not                | [^0-9] => a        |
| ^      | Start of word      | ^abc$              |
| $      | End of word        | ^abc$              |
|        |                    |                    |

## Examples

```js
/[^0-9.-]+/g
```

Matches any character not in the set 0-9, `.`, or `-`

