# Canvas

Used for 2d or 3d(WebGL) rendering 

Width and height are special attributes and introduce weird conflicts with CSS

Can be styling like any normal image(not affecting content)

```html
<canvas id="tutorial" width="150" height="150"></canvas>
```

```js
const canvas = document.getElementById('tutorial');
const ctx = canvas.getContext('2d');

```

## Beautiful Planet Example

```js
var sun = new Image();
var moon = new Image();
var earth = new Image();
function init() {
  sun.src = 'https://mdn.mozillademos.org/files/1456/Canvas_sun.png';
  moon.src = 'https://mdn.mozillademos.org/files/1443/Canvas_moon.png';
  earth.src = 'https://mdn.mozillademos.org/files/1429/Canvas_earth.png';
  window.requestAnimationFrame(draw);
}

function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');

  ctx.globalCompositeOperation = 'destination-over';
  ctx.clearRect(0, 0, 300, 300); // clear canvas

  ctx.fillStyle = 'rgba(0, 0, 0, 0.4)';
  ctx.strokeStyle = 'rgba(0, 153, 255, 0.4)';
  ctx.save();
  ctx.translate(150, 150);

  // Earth
  var time = new Date();
  ctx.rotate(((2 * Math.PI) / 60) * time.getSeconds() + ((2 * Math.PI) / 60000) * time.getMilliseconds());
  ctx.translate(105, 0);
  ctx.fillRect(0, -12, 40, 24); // Shadow
  ctx.drawImage(earth, -12, -12);

  // Moon
  ctx.save();
  ctx.rotate(((2 * Math.PI) / 6) * time.getSeconds() + ((2 * Math.PI) / 6000) * time.getMilliseconds());
  ctx.translate(0, 28.5);
  ctx.drawImage(moon, -3.5, -3.5);
  ctx.restore();

  ctx.restore();
  
  ctx.beginPath();
  ctx.arc(150, 150, 105, 0, Math.PI * 2, false); // Earth orbit
  ctx.stroke();
 
  ctx.drawImage(sun, 0, 0, 300, 300);

  window.requestAnimationFrame(draw);
}

init();
```

### Balls With Collision Example

ball.js

```js
const SPEED = 10;
import { randomColor } from "./helpers.js";

export default class Ball {
  constructor(cc, color, radius, tx, ty) {
    this.cc = cc;
    this.color = color;
    this.radius = radius;
    this.startradius = this.radius;
    this.tx = tx;
    this.ty = ty;
    this.x = Math.random() * (tx - this.radius * 2) + this.radius;
    this.y = Math.random() * (ty - this.radius * 2) + this.radius;
    this.dy = (Math.random() - 0.5) * SPEED;
    this.dx = (Math.random() - 0.5) * SPEED;
  }

  collide(balls) {
    for (let b of balls) {
      if (b === this) {
        continue;
      }

      const distX = b.x - this.x;
      const distY = b.y - this.y;
      const dist = Math.sqrt(distX * distX + distY * distY);
      const minDist = b.radius + this.radius;
      if (dist < minDist) {
        this.color = randomColor();
        const tempX = this.dx;
        this.dx = b.dx;
        b.dx = tempX;
        const tempY = this.dy;
        this.dy = b.dy;
        b.dy = tempY;
      }
    }
  }

  move(tx, ty) {
    this.tx = tx;
    this.ty = ty;
    this.y += this.dy;
    this.x += this.dx;
    if (this.y + this.radius >= this.ty || this.y - this.radius <= 0) {
      this.dy = -this.dy;
    }

    if (this.x + this.radius >= this.tx || this.x - this.radius <= 0) {
      this.dx = -this.dx;
    }
  }

  draw() {
    this.cc.beginPath();
    this.cc.arc(this.x, this.y, this.radius, 0, 2 * Math.PI);
    this.cc.fillStyle = this.color;
    this.cc.fill();
    //c.stroke();
  }
}
```

canvas.js

```js
import React, { useState, useEffect, useRef } from "react";
import PropTypes from "prop-types";

import { randomColor } from "./helpers.js";
import Ball from "./Ball.js";
const debug = require("debug")("app:Canvas");

const NUMBER_OF_BALLS = 5;
const scaleWidth = 500;
const scaleHeight = 500;

export default function Canvas() {
  const canRef = useRef(null);

  useEffect(() => {
    debug("Hello World");

    const canvas = canRef.current;
    const cc = canvas.getContext("2d");
    let tx = window.innerWidth;
    let ty = window.innerHeight;
    canvas.width = tx;
    canvas.height = ty;
    //c.lineWidth= 5;
    //c.globalAlpha = 0.5;

    let mousex = 0;
    let mousey = 0;

    addEventListener("mousemove", function () {
      mousex = event.clientX;
      mousey = event.clientY;
    });

    cc.strokeWidth = 5;

    let balls = [];
    for (let i = 0; i < NUMBER_OF_BALLS; i++) {
      balls.push(new Ball(cc, randomColor(), 50, tx, ty));
    }

    function animate() {
      debug("CW", canvas.clientWidth, "CH", canvas.clientHeight);
      if (tx != window.innerWidth || ty != window.innerHeight) {
        tx = window.innerWidth;
        ty = window.innerHeight;
        canvas.width = tx;
        canvas.height = ty;
      }
      requestAnimationFrame(animate);
      cc.clearRect(0, 0, tx, ty);
      for (let b of balls) {
        b.collide(balls);
        b.move(tx, ty);
        b.draw();

        if (
          mousex > b.x - 20 &&
          mousex < b.x + 20 &&
          mousey > b.y - 50 &&
          mousey < b.y + 50 &&
          b.radius < 70
        ) {
          //bal[i].x += +1;
          b.radius += 5;
        } else {
          if (b.radius > b.startradius) {
            b.radius += -5;
          }
        }
      }
    }

    animate();
  }, []);

  return <canvas className="border border-black w-full h-64" ref={canRef} />;
}
```

