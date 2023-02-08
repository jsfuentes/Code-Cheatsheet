# ASDF

Version manager with offical support for Node, Elixir, Erlang, and Ruby. Community plugins for more.

## Install ASDF

https://asdf-vm.com/guide/getting-started.html#core-installation-complete

## Install New Versions Plugins

```bash
asdf list all elixir #list all versions
asdf list all erlang
asdf install nodejs latest #install
```

#### List installed Versions

```bash
asdf list <name> #list all installed versions
```

#### Change Version

```bash
asdf global nodejs latest #set
asdf local nodejs 11.6
```



## Add New Plugin

```bash
asdf plugin add python

asdf install python latest
asdf global python latest
#OR
asdf install python 3.7.9
asdf global python 3.7.9
```

## ### See Installed Plugins

```bash
asdf plugin list
```



```bash
brew upgrade asdf
asdf exec python #to run bash scripts in the asdf env
```

