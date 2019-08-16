# General

- [React Loaders] - https://jonjaques.github.io/react-loaders/

  - ```bash
    npm i --save react-loaders loaders.css
    ```

    ```js
    import Loader from 'react-loaders';
    let loader = <Loader type="ball-pulse" />;
    ```

  - ```css
    $primary-color: $my-brand-color;
    @import 'loaders.css/src/animations/ball-pulse.scss'
    
    .loader-hidden {
      display: none;
    }
    .loader-active {
      display: block;
    }
    ```

  - 