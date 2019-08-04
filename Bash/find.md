# Find

recursively descends the directory tree for each path listed, evaluating an expression

*wont follow soft links* 

### Find file with word in them

```bash
find . -iname [word]
find . -iname local # => ./Projects/local
```

#### Find some string in all files in cur dir

```bash
find . -type f -print0 | xargs -0 
# OR
grep "some string"
```

