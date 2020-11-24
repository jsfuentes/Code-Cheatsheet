#  Position

There are five different position values:

- `static`(default)
  - Width constrained to parents bounding box
  - not affected by z-index

## Moving

If not static, elements are then positioned using the top, bottom, left, and right properties

- `relative` - adjusted away from normal pos, does nothing if t/b/l/r not set
- `fixed` - positioned relative to the viewport, sticks to position on scroll
- `absolute` 
  - relative to the nearest ancestor with a nonstatic position set or viewport if none
  - Removes it from the document flow so other divs will be rendered as if it wasnt there
- `sticky` - relative until it would be out of viewport then fixed

