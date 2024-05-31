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
| Shift-Alt-O | Delete Unused Imports       |
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
  "My API Service Function": {
    "prefix": "myapi",
    "body": [
      "interface ${1/(^.)/${1:/upcase}/}Response {",
      "  data: Board;",
      "}",
      "",
      "async function $1($2) {",
      "  try {",
      "    const resp = await axios.post<${1/(^.)/${1:/upcase}/}Response>(\"/api/boards\", { $2 });",
      "    return resp.data;",
      "  } catch (err) {",
      "    store.dispatch(logAxiosError(err, $3));",
      "    throw err;",
      "  }",
      "}"
    ]
  }
```

- \$1, \$2 to specify cursor locations. The number is the order in which tabstops will be visited, whereas \$0 
- also has variables like time, date, filename, etc
- Can transform variables like `${1/(^.)/${1:/upcase}/` to uppercase first letter so capture then specific what to do to it

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

