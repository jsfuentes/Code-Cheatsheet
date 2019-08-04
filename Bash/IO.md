# IO in Bash

Each open file gets assigned a file descriptor.	[[2\]](https://www.tldp.org/LDP/abs/html/io-redirection.html#FTN.AEN17894) The file descriptors for `stdin`, `stdout`, and `stderr` are 0, 1, and 2, respectively.

## Basics

| Command                         | do                                               |                                |
| ------------------------------- | ------------------------------------------------ | ------------------------------ |
| [cmd] > [filename]              | Redirects stdout to file creating or overwriting | echo "hi" > test.txt           |
| [cmd] >> [filename]             | Appends stdout to file if it exists, or creates  | echo "Thank you" >> test.txt   |
| 1>[filename]                    | redirect stdout to file                          | echo "Dream better" 1>$LOGFILE |
| 2>[filename]                    | redirect stdeer                                  | bad_command1 2>$ERRORFILE      |
| &>[filename]  ORR  >&[filename] | redirect both stdout and stderr                  |                                |
| 0< FILENAME                     | accept input from a file                         |                                |

### Pipes

General purpose comman chaining 

cat *.txt | sort | uniq > test.txt

## Advanced Stupid Stuff

| Cmd            | do                          | Ex           |
| -------------- | --------------------------- | ------------ |
| : > [filename] | make file empty             | : > test.txt |
| 2>&1           | Redirects stderr to stdout. |              |

