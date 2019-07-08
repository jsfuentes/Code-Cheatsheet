Makefile

Makefile name

```makefile
CC=gcc
CFLAGS=-I.
DEPS = hellomake.h

%.o: %.c $(DEPS)
	$(CC) -c -o $@ $< $(CFLAGS)

hellomake: hellomake.o hellofunc.o 
	$(CC) -o hellomake hellomake.o hellofunc.o
```

## Differences From Bash

- It seems \$PWD works instead of ​\$(pwd) within a command
- To do command after a cd, use semicolon

```makefile
cd ./client; yarn build;
```



 

