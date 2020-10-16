# Matter

```bash
yarn add matter-attractors matter-js matter-wrap
```

--------

Physics engine on canvas

```jsx
import React, { useState, useEffect, useContext, useRef } from "react";
import ReactDOM from "react-dom";
import Matter from "matter-js";
import MatterAttractors from "matter-attractors";
import MatterWrap from "matter-wrap";
import PropTypes from "prop-types";

import { randomColor } from "src/utils/helpers";
import { isMobile } from "src/utils/utils";
const debug = require("debug")("app:LandingViz");

let BALL_COUNT = 150;
if (isMobile) BALL_COUNT = 50;
const BALL_MIN_RADIUS = 10;
const BALL_MAX_RADIUS = 16;
const BALL_SPEED = 1;

const Engine = Matter.Engine,
  Render = Matter.Render,
  World = Matter.World,
  Body = Matter.Body,
  Bodies = Matter.Bodies,
  Mouse = Matter.Mouse,
  Vector = Matter.Vector,
  Runner = Matter.Runner,
  Common = Matter.Common,
  Composite = Matter.Composite,
  MouseConstraint = Matter.MouseConstraint;

Matter.use(MatterAttractors);
Matter.use(MatterWrap);
MatterAttractors.Attractors.gravityConstant = 0.0001;

export default function LandingViz(props) {
  const tableRef = useRef(null);

  function addCircles(world, render) {
    for (let i = 0; i < BALL_COUNT; i++) {
      const radius = Common.random(BALL_MIN_RADIUS, BALL_MAX_RADIUS);

      const body = Bodies.circle(
        Common.random(BALL_MIN_RADIUS, render.options.width),
        Common.random(BALL_MIN_RADIUS, render.options.height),
        radius,
        {
          mass: Common.random(BALL_MIN_RADIUS, BALL_MAX_RADIUS),
          frictionAir: 0,
          render: {
            fillStyle: randomColor(),
            // strokeStyle: "#FFFFFF",
          },
          plugin: {
            attractors: [
              // there is a built in helper function for Newtonian gravity!
              // you can find out how it works in index.js
              MatterAttractors.Attractors.gravity,
            ],
            wrap: {
              min: { x: 0, y: 0 },
              max: { x: render.options.width, y: render.options.height },
            },
          },
        }
      );

      Body.setVelocity(body, {
        x: Common.random(-BALL_SPEED, BALL_SPEED),
        y: Common.random(-BALL_SPEED, BALL_SPEED),
      });

      World.add(world, body);
    }
  }

  useEffect(() => {
    setTimeout(() => {
      const CANVAS_WIDTH = tableRef.current.clientWidth;
      const CANVAS_HEIGHT = tableRef.current.clientHeight;

      const engine = Engine.create();
      engine.world.gravity.scale = 0;

      const render = Render.create({
        element: tableRef.current,
        engine: engine,
        options: {
          width: CANVAS_WIDTH,
          height: CANVAS_HEIGHT,
          background: "transparent",
          wireframes: false,
        },
      });

      const runner = Runner.create();
      Runner.run(runner, engine);
      Render.run(render);

      addCircles(engine.world, render);

      // // add mouse control
      // const mouse = Mouse.create(render.canvas),
      //   mouseConstraint = MouseConstraint.create(engine, {
      //     mouse: mouse,
      //     constraint: {
      //       stiffness: 0.2,
      //       render: {
      //         visible: false,
      //       },
      //     },
      //   });
      // World.add(engine.world, mouseConstraint);

      // Matter.Events.on(mouseConstraint, "mousedown", function (event) {
      //   addCircle(engine.world);
      // });

      // mouseConstraint.mouse.element.removeEventListener(
      //   "mousewheel",
      //   mouseConstraint.mouse.mousewheel
      // );
      // mouseConstraint.mouse.element.removeEventListener(
      //   "DOMMouseScroll",
      //   mouseConstraint.mouse.mousewheel
      // );

      Engine.run(engine);

      return () => {
        Matter.Render.stop(render);
        Matter.Runner.stop(runner);
      };
    }, 1500);
  }, []);

  return <div className="w-full h-full" ref={tableRef} />;
}

```

