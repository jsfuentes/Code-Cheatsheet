## Positioning

### Grid

```react
<div class="grid grid-cols-4 gap-4">
  <div>01</div>
  <!-- ... -->
  <div>09</div>
</div>
```

#### Flex

##### Cross-Axis

.items-stretch (default?)  | .items-start  | .items-center  | .items-end  | .items-baseline  |

##### Main-Axis

Justify-start | justify-center | justify-end | justify-between | justify-around

```html
<div className="flex flex-col justify-center items-center mt-4 lg:mt-36 mb-20 lg:mb-28">
  <div> Tails </div>
  <div> Sonic </div>
</div>
```

#### Position

.static | .fixed | .absolute | .relative | .sticky

```html
<div class="absolute top-0 right-0 bg-gray-800">
  
</div>
```

## 