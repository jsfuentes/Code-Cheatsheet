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

## Packages



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

#### Code to Snippets Script

```python
name = "Express Router Boilerplate"
prefix = "myroute"
code = """const express = require("express");
const debug = require("debug")("app:routes:folder");

const Folder = require("../models/Folder.js");
const asyncH = require("../utils/asyncHandler.js");

let router = express.Router();

router.get("/", asyncH(getFolder));

async function getFolder(req, res) {
  const f = await Folder.find().exec();
  debug(f, typeof f);
  res.json(f);
}

module.exports = router;"""

def cleanLine(l):
  newL = "\t\t\""
  for c in l:
    if c == "\"":
      newL += "\\"
      newL += c
    elif c == "\t":
      newL += "\\t"
    else:
      newL += c
  newL += "\","
  return newL

bs = "{"
be = "}"
print(f"\"{name}\": {bs}")
print(f"\t\"prefix\": \"{prefix}\",")
print("\t\"body\": [")
for line in code.split("\n"):
  print(cleanLine(line))
print("\t]")
print(be + ",")
```

