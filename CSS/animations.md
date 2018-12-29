# Animations

Instead of one transition with transitions, can have up to an infinite number of iterations, grandular control

- @keyframes
- animation-name
- animation-duration
- animation-timing-function
- animation-iteration-count
- animation-direction
- animation-play-state
- animation-delay
- animation-fill-mode
- animation (shorthand)

## @Keyframe

```css
@keyframes clever_name_here ...
```

```css
@keyframes writing {
    from { /*same as 0%*/
        left: 0;
    }
    
    to { /*same as 100%*/
        left: 100%;
    }
}
```

- % basically the total animation time
- !important not important in animations
- It repaints the page when you change left/top, should use transform 

```css
/*zigzag across screen*/
@keyframes w {
    0% {
        left: 0;
        top: 0;
    }
    25%, 75% {
        top: 400px;
    }
    50% {
        top: 50px;
    }
    100% {
        left: 80%;
        top: 0;
    }
}
```

### Using Keyframe

- By default happens once
- Can have multiple animations happening on same element at same time, last declared animation overrides other props if same props

```css
.pencil {
	animation-name: w;
    animation-duration: 3s;
}
```

## Timing Function

linear |ease-in-out|ease-in|ease-out|step-start|step-end|ease|steps(X, start|**end**)|cubic-bezier(x1, y1, x2, y2) 

- [see how it looks](cubic-bezier.com)

### Steps

Discrete steps

start/end is which frame you drop i.e 2-4-6-8-10 or 0-2-4-6-8-10

Sprites(is a strip animate with:), add second animation to make it move across screen

```css
.biker {
  height: 92px;
  width: 90px;
  background-image: url(../static/img/bike.png);
  background-repeat: no-repeat;
  animation: pedal 400ms steps(4, end) infinite; 
}
@keyframes pedal { 
    100% {background-position: -360px 0;}
}
```

## Iteration-count

Can even do partial count so cuts off

## Animation-delay

Can even do negative and skips in animation time

## Animation-Direction

normal | alternate|reverse|alternate-reverse

## Animation(shorthand)

name duration delay timing-function iteration-count

```css
.pencil {
    animation: test 5s ease-in-out 100ms 5;
}
```

## Animation Fill Mode

None | forwards | backwards | both

What do after last animation? 

- None: go back
- forwards: keep at 100%
- backwards: keep at 0% during animation delay/start

### Play-state

 ```css
.pencil:hover{
    Animation-play-state: paused;
}
 ```

Running | paused

## Events

- animationstart
- animationend
- animationiteration

Can add and remove class of animation at animation end to restart event(put slight delay on regiving class)

