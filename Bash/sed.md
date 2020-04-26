# Sed

Stream editor to do bash text manipulation

### String Substituting

First one hit

```bash
sed 's/hello/world/' input.txt > output.txt
```

Translate all

```bash
echo "hello hello my world world" | sed 's/hello/world/g'
```

