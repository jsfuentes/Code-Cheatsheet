# Featured Shortcuts

## VSCode Navigation

| Command     | Result                      |
| ----------- | --------------------------- |
| Cmd-Shift-P | Command Palette             |
| Cmd-P       | Open a File                 |
| Cmd-T       | Find class, ft, or variable |
| Cmd-Shift-E | Explorer Open               |
| Cmd-K Cmd-W | Close all open files        |
| Cmd-B       | Toggle SidePanel            |
|             |                             |
|             |                             |
|             |                             |

## Editor Navigation

| Cmd         | Result              |
| ----------- | ------------------- |
| Cmd-L       | Select Current Line |
| Cmd-Shift-K | Delete Current Line |
|             |                     |

## Install Shell

Open the **Command Palette** (⇧⌘P) and type 'shell command'

### Snippets

Use them Cmd-Shift-P snippets to configure something like below:

```json
	"React Hooks Component Boilerplate": {
		"prefix": "myre",
		"body": [
			"import React, { useEffect, useState } from \"react\";",
			"import PropTypes from \"prop-types\";",
			"",
			"function $1(props) {",
			"\t$2",
			"\treturn ()",
			"}",
			"",
			"$1.propTypes = {",
			"\t",
			"}",
			"export default $1;"
		]
	}
```

- \$1, \$2 to specify cursor locations. The number is the order in which tabstops will be visited, whereas \$0 