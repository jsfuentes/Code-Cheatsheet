# Transforms

## 2D Transform

- translate
- scale
- rotate
- skew
- Matrix
- Have X and Y specific ones for each

```css
.letters {
    transform: 
    	translate(-90px, 0px), 	/*hor, ver*/			rotate(90deg), scale(0.25, 0.75),/*w, h*/
        skew(5deg, 5deg)
        
}
```

Can use any of these, this order does matter and each operation is done in that order. Recall graphics/matrix manipulation translating than rotating is different from rotating than translating. Rotates about center of image though not origin, and translates on its current axises

## 3D Transform

- translate3d
- scale3d
- rotate3d
- matrix3d
- perspective: none | length(in px from eyeball)
- **Transform-origin**: length | keyterm(1, 3)  where do you rotate/transform from i.e(`top left` then rotate rotates about top left corner )
- transform-style: flat | preserve-3d how to handle nested elements
- Perspective-origin: pos relative to viewer(i.e top left)
- Backface-visibility: visible | hidden do you show back of image if rotated

3D requires perspective goes first in transform or can be sole attribute by parent

