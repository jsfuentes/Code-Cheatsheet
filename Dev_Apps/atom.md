# Featured Shortcuts

| Command             | Result                       |
| ------------------- | ---------------------------- |
| Cmd-Shift-/         | Find in file tree            |
| Cmd-Click           | Go to Declaration            |
| Opt-O               | Outline View for Large Files |
| Alt-B               | Beginning of word Atom       |
| Alt-F               | End of word Atom             |
| Command-Shift-P     | Master Command Atom          |
| Command-Opt-I       | Open Inspection              |
| Opt-Shift-K         | Delete Line                  |
| Command-Shift-P tca | Close all Tabs               |

## Packages

| Result          | Command    |
| --------------- | ---------- |
| Beautify-editor | ctrl-alt-b |
|                 |            |

## Snippets

Quickly type large amounts of code by typing shortcut then pressing tab

Go to Atom in top bar, snippets, and follow instructions

```cson
'.source.js':
  'console.log':
    'prefix': 'log'
    'body': 'console.log(${1:"crash"});$2'
```

So typing `log[tab]` would expand it to console.log("crash");

first tab press selects crash 

second tab press places cursor at end 

Use `"""` for multiple line