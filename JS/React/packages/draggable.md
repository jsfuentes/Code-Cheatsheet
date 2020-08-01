# Draggable

```bash
yarn add react-draggable
```

Use transforms so can just wrap in the div and it works

## Usage

bounds can also be parent, or no bounds and can go anywhere

```jsx
        <Draggable bounds="#basic-tile-draggable-container">
          <div
            className="absolute right-1 bottom-0"
            style={{
              width: Math.floor(width / 7),
              height: Math.floor(height / 7),
            }}
          >
            <VideoBubble
              callItem={subItem}
              playAudio={false}
              monitorAudio={true}
              showName={false}
            />
          </div>
        </Draggable>
```

