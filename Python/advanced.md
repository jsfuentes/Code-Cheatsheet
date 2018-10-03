# Advanced Stuff

- `globals()` *always* returns the dictionary of the *module* namespace
- `locals()` *always* returns *a* dictionary of the *current* namespace

print(locals()) will let you do some easy debugging (in fts, extra stuff in global namespace)