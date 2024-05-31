# ASDF

Version manager with offical support for Node, Elixir, Erlang, and Ruby. Community plugins for more.

```bash
brew install asdf
```

## Install ASDF

https://asdf-vm.com/guide/getting-started.html#core-installation-complete

## Install New Versions Plugins

```bash
asdf list all elixir #list all versions
asdf list all erlang
asdf install nodejs lts-iron #install
```

#### List installed Versions

```bash
asdf list <name> #list all installed versions
```

#### Change Version

```bash
asdf global nodejs lts-iron #set
asdf local nodejs lts-iron
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

## See Installed Plugins

```bash
asdf plugin list
```



```bash
brew upgrade asdf
asdf exec python #to run bash scripts in the asdf env
```

## Debugging

ERROR:

```
Please install a version by running one of the following:

asdf install nodejs 18.19.0

or add one of the following versions in your config file at /Users/jfuentes/.tool-versions
nodejs 16.14.0
```

SOLUTION:

- Try `asdf reshim nodejs`
- Try `asdf current nodejs` to see where its getting the version from
- After reshimming/installing/changing, may need to refresh terminal
- Perhaps the tool you are trying to run is installed under the wrong version, `npm install -g @aws-amplify/cli` in the current node version fixed it for me
