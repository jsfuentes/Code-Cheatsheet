# Essential Middleware

[Common Express Middleware](<https://expressjs.com/en/resources/middleware.html>)

- body-parser: parses request bodies for POST parameters.

  - ```js
    const bodyParser = require('body-parser');
    app.use(bodyParser.json());
    ```
  
    - builtin express.json() will work for most cases, bodyParser works when raw json text in postman with single quotes while express.json wont
  
- cookie-parser: Used to parse the cookie header and populate req.cookies (essentially provides a convenient method for accessing cookie information).

  - ```js
    const cookieParser = require("cookie-parser");
    app.use(cookieParser());
    ```

- cors: Enable cross origin stuff globally

  - ```js
    const cors = require("cors");
    app.use(cors());
    ```

- morgan: An HTTP request logger middleware for node.

  - ```js
    app.use(morgan('dev'))
    //=> GET / 200 17.199 ms - -
    ```

- serve-favicon: Node middleware for serving a favicon (this is the icon used to represent the site inside the browser tab, bookmarks, etc.).

  