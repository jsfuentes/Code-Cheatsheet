# Tmux

tmux is a terminal multiplexer that keeps your session running even when your computer loses its connection to the devserver.

You can have multiple **sessions** that can hold multiple **windows** 

Can do multi-screens of tmux and like ide stuff or something idk.... 

## Sessions

| `tmux attach`        | access previous session                      |
| -------------------- | -------------------------------------------- |
| `tmux`               | new session                                  |
| `tmux ls`            | list all sessions                            |
| `tmux attach -t [0]` | access specific session given number from ls |
| `exit`               | exit current session                         |

## Windows/Tabs

`Ctrl-b` base command 

| `c`  | create window   |
| ---- | --------------- |
| `&`  | kill window     |
| `n ` | next window     |
| `p`  | previous window |
| `f`  | find window     |
| `,`  | name window     |
| `w`  | list windows    |

## Panes Within a Window

`Ctrl-b` base command 

| %    | horizontal split  |
| ---- | ----------------- |
| ""   | vertical split    |
| o    | swap panes        |
| q    | show pane numbers |
| x    | kill pane         |

