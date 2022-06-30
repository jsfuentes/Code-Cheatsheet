# Background

Background

- -color 
- -image: none | <uri> | inherit
- -repeat
- -attachment
- -position
- -clip
- -origin
- -size
- background

### Background-image

```css
background-image: url(path/aSingleImage.jpg);
```

- linear-gradient(to bottom, green, blue)
- url(s.png), url(s.jpg)
- url(data:image/gid; base64, ajfksljv24..)
- element('#myID')

Often want to use background color if image doesnt load

can do comma seperated images then image you declare first on top

Not fully supported: 

- *crossfade(* & *image(*
- url(sprite.png#xywh=40,0,20,20) #shows specific part of image, ignored in unsupported browser 

### Background-repeat

repeat|repeat-x|repeat-y|no-repeat |space | round 

Space has no cutoff background images

Round changes size of image to take up all space, no cutoff

### Background-attachment

if you scroll within section, what happens

### background-position

```css
background-position: 90% 90%;
background-position: bottom 90% right 90%; 
background-position: center;
/*can do px too; 90% from bottom and right*/
```

puts 90%, 90% of image in 90% of 90% of entire background

### Background-clip

where do you start background color

*Content-box:* dont put background around padding

*padding-box*: put background around padding

*Border-box*: put background behind border

### background-origin

where do you start background image; same values as above

Doesn't draw background image where it doens't color background, so cut off image

### background-size

Auto: size image was naturally

contain: grows or shrinks to fit in 1d maintaining ratio

cover: grows to min size that cover 100% of height&width maintaining ratio
<length>: grow image to length

### background

Don't use it has too many properties and changes defaults

## Extra

### Opacity

Can set `opacity: .03` to parent div, but the children text also inherit it and makes text hard to read

Can just use rgba background: rgba(76, 175, 80, 0.3)