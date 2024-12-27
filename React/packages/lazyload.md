# [React Lazy Load](https://www.npmjs.com/package/react-lazyload)

```
yarn add react-lazyload
```

## Usage

```react
import React, { useState, useEffect, useRef } from "react";
import LazyLoad from "react-lazyload";
import classNames from "classnames";
import PropTypes from "prop-types";

const debug = require("debug")("app:LazyImage");

LazyImage.propTypes = {
  src: PropTypes.string,
  height: PropTypes.string,
  width: PropTypes.string,
  alt: PropTypes.string,
  className: PropTypes.string,
  imgCls: PropTypes.string,
  style: PropTypes.object,
  darkMode: PropTypes.bool,
};

export default function LazyImage(props) {
  const { src, height, width, alt, className, darkMode, imgCls } = props;

  return (
    <div className={`${className}`} style={props.style}>
      <LazyLoad
        classNamePrefix="relative w-full "
        offset={300}
        height={height}
        width={width}
        overflow
        resize
        once
      >
        <MyImage
          src={src}
          height={height}
          width={width}
          alt={alt}
          darkMode={darkMode}
          imgCls={imgCls}
        />
      </LazyLoad>
    </div>
  );
}

//Must be in seperate component so can listen to when the LazyLoad mounts it
MyImage.propTypes = {
  src: PropTypes.string,
  height: PropTypes.string,
  width: PropTypes.string,
  alt: PropTypes.string,
  style: PropTypes.object,
  darkMode: PropTypes.bool,
  imgCls: PropTypes.string,
};

function MyImage(props) {
  const { src, height, width, alt, style, darkMode, imgCls } = props;
  const [loaded, setLoaded] = useState(false);
  const imgR = useRef(null);

  useEffect(() => {
    const img = imgR.current;
    function setLoadedTrue() {
      setLoaded(true);
    }

    if (img) {
      img.addEventListener("load", setLoadedTrue);

      if (img.complete) {
        //if already loaded
        setLoaded(true);
      }

      return () => img.removeEventListener("load", setLoadedTrue);
    }
  }, []);

  const cls = classNames({
    "absolute w-full h-full left-0 top-0 right-0 bottom-0 z-10 transition-opacity duration-500 ease-in-out ": true,
    "opacity-0": loaded,
    "opacity-100": !loaded,
    "bg-pureBlack": darkMode,
    "bg-white": !darkMode,
  });

  return (
    <>
      <div className={cls} />
      <img
        src={src}
        height={height}
        width={width}
        alt={alt}
        ref={imgR}
        style={style}
        className={imgCls}
      />
    </>
  );
}

```

