## Columns

```css
column-count: 6;
column-width: 5em;
column-rule: 1px solid #bbb;
column-gap: 2em;
```

- Max column count and min column width 
- If words are too long, then colun gap won't work
- column rule is line between columns

## Put Header 

```css
#content { Columns: 8em 3; } 
h1 {column-span: all;}
```

 At least 8 em, but not more than 3 cols

A h1 will span all the columns 