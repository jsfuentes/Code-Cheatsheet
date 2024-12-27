# [React-window](https://addyosmani.com/blog/react-window/)

Adds windowing to lists so it is much more efficient

```
yarn add react-window
```

## Example

```react
// These column widths are arbitrary.
// Yours should be based on the content of the column.
const columnWidths = new Array(1000)
  .fill(true)
  .map(() => 75 + Math.round(Math.random() * 50));

const getItemSize = (index) => columnWidths[index];

const Column = ({ index, style }) => (
  <div style={style} className="font-white">
    Column {index}
  </div>
);

const Example = () => (
  <List height={600} itemCount={1000} itemSize={getItemSize} width={150}>
    {Column}
  </List>
);
```

### Autosize

Use FixedSizeList if all elements same size, else use VariableSizeList which expects a function for size

```react
import { FixedSizeList as List } from "react-window";
import AutoSizer from "react-virtualized-auto-sizer";

const Row = ({ index, style }) => (
  <div className={index % 2 ? "ListItemOdd" : "ListItemEven"} style={style}>
    Row {index}
  </div>
);

const Example = () => (
  <AutoSizer>
    {({ height, width }) => (
      <List
        className="List"
        height={height}
        itemCount={1000}
        itemSize={35}
        width={width}
      >
        {Row}
      </List>
    )}
  </AutoSizer>
);

```

