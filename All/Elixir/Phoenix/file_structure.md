# Default File Structure

- Can make a plug folder in web and then include in router.ex
- Can import things in discuss_web.ex that will then be available in all views/controllers

├── build
├── assets
├── config
├── deps
├── lib
       └── hello
       └── hello_web
       └── hello.ex
       └── hello_web.ex
├── priv
├── test

Lib/hello_web

```
├── channels
│   └── user_socket.ex
├── controllers
│   └── page_controller.ex
├── templates
│   ├── layout
│   │   └── app.html.eex
│   └── page
│       └── index.html.eex
└── views
│   ├── error_helpers.ex
│   ├── error_view.ex
│   ├── layout_view.ex
│   └── page_view.ex
├── endpoint.ex
├── gettext.ex
├── router.ex
```

