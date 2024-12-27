# Slate

A text-editor framework built with React

```bash
yarn add slate slate-react
```

#### Concepts

- Slate is pure JSON objects and any custom properties/actions are up to you, then you can render based on those custom properties
- Root Editor node, container element nodes, and leaf level text nodes form a tree just like a DOM
- Paths refer to node, points are a path and offset, and ranges have an anchor(start) and focus(end)

### Basic Usage

```jsx
import React, { useEffect, useMemo, useState } from "react";
import { createEditor } from 'slate';
import { Slate, Editable, withReact } from 'slate-react'

const App = () => {
  // Want editor to be stable across renders 
  const editor = useMemo(() => withReact(createEditor()), []);
  const [value, setValue] = useState([
    {
      type: 'paragraph',
      children: [{ text: 'A line of text in a paragraph.' }],
    },
  ]);

  //create shared Slate context
  return (
    <Slate editor={editor} value={value} onChange={value => setValue(value)}>
      <Editable />
    </Slate>
  )
}
```

### Event Handlers

```jsx
  return (
    <Slate editor={editor} value={value} onChange={value => setValue(value)}>
      <Editable
       onKeyDown={event => {
          if (event.key === '&') {
            // Stop ampersand insertion
            event.preventDefault()
            editor.insertText("and")
          }
        }}
      />
    </Slate>
  )
```

### Custom Blocks

Default internal renderer is just div. Element renderers are just simple React components. Must render children as lowest leaf in component

```jsx
const CodeElement = props => {
  return (
    <pre {...props.attributes}>
      <code>{props.children}</code>
    </pre>
  )
}

const DefaultElement = props => {
  return <p {...props.attributes}>{props.children}</p>
}
```

Use `Transforms` and events to enter the code block and the `renderElement` ft to alter it

```jsx
import { Editor, Transforms } from 'slate'

//....
function App() {
  //............
 // Change renderer based on props
  const renderElement = useCallback(props => {
    switch (props.element.type) {
      case 'code':
        return <CodeElement {...props} />
      default:
        return <DefaultElement {...props} />
    }
  }, [])
  
    return (
    <Slate editor={editor} value={value} onChange={value => setValue(value)}>
      <Editable
        renderElement={renderElement}
        onKeyDown={event => {
            if (event.key === "`" && event.ctrlKey) {
              debug("ACTIVATE BLASTOFF");
              event.preventDefault();
              // Determine whether any of the currently selected blocks are code blocks.
              const [match] = Editor.nodes(editor, {
                match: (n) => n.type === "code",
              });
              // Toggle the block type depending on whether there's already a match.
              Transforms.setNodes(
                editor,
                { type: match ? "paragraph" : "code" },
                { match: (n) => Editor.isBlock(editor, n) }
              );
            }
        }}
      />
    </Slate>
  )
```

### Custom Formatting

```jsx
  const renderLeaf = useCallback(props => {
    return <Leaf {...props} />
  }, [])
	//......
		<Editable
        renderElement={renderElement}
        renderLeaf={renderLeaf}
        onKeyDown={event => {
    			if(event.key === "b" && event.ctrlKey) {
            event.preventDefault();
            Transforms.setNodes(
              editor,
              { bold: true },
              // Apply it to text nodes, and split the text node up if the
              // selection is overlapping only part of it.
              { match: (n) => Text.isText(n), split: true }
            );
          }
  			}}
        />
```

Slate breaks up text into **leaves**

```jsx
// Define a React component to render leaves with bold text.
const Leaf = props => {
  return (
    <span
      {...props.attributes}
      style={{ fontWeight: props.leaf.bold ? 'bold' : 'normal' }}
    >
      {props.children}
    </span>
  )
}
```

### Executing Commands

Augment editor object to handle your own rich text commands or use plugins, extracting lets you make a toolbar too

Everything put togther above, but using custom commands

```jsx
const App = () => {
  const editor = useMemo(() => withReact(createEditor()), [])
  const [value, setValue] = useState([
    {
      type: 'paragraph',
      children: [{ text: 'A line of text in a paragraph.' }],
    },
  ])

  const renderElement = useCallback(props => {
    switch (props.element.type) {
      case 'code':
        return <CodeElement {...props} />
      default:
        return <DefaultElement {...props} />
    }
  }, [])

  const renderLeaf = useCallback(props => {
    return <Leaf {...props} />
  }, [])

  return (
    // Add a toolbar with buttons that call the same methods.
    <Slate editor={editor} value={value} onChange={value => setValue(value)}>
      <div>
        <button
          onMouseDown={event => {
            event.preventDefault()
            CustomEditor.toggleBoldMark(editor)
          }}
        >
          Bold
        </button>
        <button
          onMouseDown={event => {
            event.preventDefault()
            CustomEditor.toggleCodeBlock(editor)
          }}
        >
          Code Block
        </button>
      </div>
      <Editable
        editor={editor}
        renderElement={renderElement}
        renderLeaf={renderLeaf}
        onKeyDown={event => {
          if (!event.ctrlKey) {
            return
          }

          switch (event.key) {
            case '`': {
              event.preventDefault()
              CustomEditor.toggleCodeBlock(editor)
              break
            }

            case 'b': {
              event.preventDefault()
              CustomEditor.toggleBoldMark(editor)
              break
            }
          }
        }}
      />
    </Slate>
  )
}
```

### Saving to a Database

Just use JSON.stringify/JSON.parse on the value.

```jsx
const App = () => {
  const editor = useMemo(() => withReact(createEditor()), [])
  const [value, setValue] = useState(    JSON.parse(localStorage.getItem('content')) || [
      {
        type: 'paragraph',
        children: [{ text: 'A line of text in a paragraph.' }],
      },
    ])

  return (
    <Slate
      editor={editor}
      value={value}
      selection={selection}
      onChange={value => {
        setValue(value)
        // Save the value to Local Storage.
        const content = JSON.stringify(value)
        localStorage.setItem('content', content)
      }}
    >
      <Editable />
    </Slate>
  )
}
```

## Editor

Commands act if user was performing, so happen at cursor

```js
interface Editor {
  children: Node[]
  selection: Range | null
  operations: Operation[]
  marks: Record<string, any> | null
  // Schema-specific node behaviors.
  isInline: (element: Element) => boolean
  isVoid: (element: Element) => boolean
  normalizeNode: (entry: NodeEntry) => void
  onChange: () => void

  // Overrideable core actions.
  addMark: (key: string, value: any) => void
  apply: (operation: Operation) => void
  deleteBackward: (unit: 'character' | 'word' | 'line' | 'block') => void
  deleteForward: (unit: 'character' | 'word' | 'line' | 'block') => void
  deleteFragment: () => void
  insertBreak: () => void
  insertFragment: (fragment: Node[]) => void
  insertNode: (node: Node) => void
  insertText: (text: string) => void
  removeMark: (key: string) => void
}
```

Custom commands

```jsx
const MyEditor = {
  ...Editor,

  insertParagraph(editor) {
    // ...
  },
}
```

## Transforms

```jsx
// Set a "bold" format on all of the text nodes in a range.
Transforms.setNodes(
  editor,
  { bold: true },
  {
    at: range,
    match: node => Text.isText(node),
    split: true,
  }
)

// Wrap the lowest block at a point in the document in a quote block.
Transforms.wrapNodes(
  editor,
  { type: 'quote', children: [] },
  {
    at: point,
    match: node => Editor.isBlock(editor, node),
    mode: 'lowest',
  }
)

// Insert new text to replace the text in a node at a specific path.
Transforms.insertText(editor, 'A new string of text.', { at: path })

// ...there are many more transforms!
```

### Operations

Lower level version of everything that can happen to doc, not extensible

```js
editor.apply({
  type: 'insert_text',
  path: [0, 0],
  offset: 15,
  text: 'A new string of text to be inserted.',
})

editor.apply({
  type: 'remove_node',
  path: [0, 0],
  node: {
    text: 'A line of text!',
  },
})

editor.apply({
  type: 'set_selection',
  properties: {
    anchor: { path: [0, 0], offset: 0 },
  },
  newProperties: {
    anchor: { path: [0, 0], offset: 15 },
  },
})
```

