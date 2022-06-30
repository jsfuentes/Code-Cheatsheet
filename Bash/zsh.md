# ZSH

the Z shell, the default on Mac OS since 10.15 Catalina

Run below install much needed good default config oh my zsh:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

Mostly same shell as bash but also:

- **Automatic cd:** Just type the name of the directory( [`setopt auto_cd`](http://zsh.sourceforge.net/Doc/Release/Options.html#index-AUTO_005fCD))
- **Recursive path expansion:** For example “/u/lo/b” expands to “/usr/local/bin”
- **Spelling correction and approximate completion:** If you make a minor mistake typing a directory name, ZSH will fix it for you
- **Plugin and theme support:** ZSH includes many different plugin frameworks
- **[Glob qualifiers](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Glob-Qualifiers)** allow matching files based on metadata such as their time stamp, their size, etc
- `alias` to show all aliases

## Breaking Differences

- **.zprofile** is equivalent to **.bash_profile** and runs at login, including over SSH
- **.zshrc** is equivalent to **.bashrc** and runs for each new Terminal session
- You can't just copy files because you many configs need tweaking :(
- Mostly same, but many minor differences in including prompt, key bindings, completion and command line history

## Zsh Themes

```zsh
ZSH_THEME="agnoster" 
ZSH_THEME="spaceship"
ZSH_THEME="af-magic"
```

### Spaceship

https://github.com/denysdovhan/spaceship-prompt

- Sigma/plugin on  master [$!?] is 📦 v1.0.0 via ⬢ v12.14.1

### Agnoster

Add `prompt_context(){}` at bottom of .zshrc to get rid of machine text on local machine

Might need to install fonts if all the emojis don't print: `echo "\ue0b0 \u00b1 \ue0a0 \u27a6 \u2718 \u26a1 \u2699"`

```
git clone https://github.com/powerline/fonts.git --depth=1
cd fonts
./install.sh
cd ..
rm -rf fonts
```

And then go into iterm and change the font to one of the newly installed fonts(Courier for proline?)

### Different Profiles

How I choose where to put a setting

- if it is needed by a **command run non-interactively**(environment variables): `.zshenv`
- if it should be **updated on each new shell**: `.zshenv`
- if it runs a command which **may take some time to complete**: `.zprofile`
- if it is related to **interactive usage**(alias): `.zshrc`
- if it is a **command to be run when the shell is fully setup**: `.zlogin`
- if it **releases a resource** acquired at login: `.zlogout`