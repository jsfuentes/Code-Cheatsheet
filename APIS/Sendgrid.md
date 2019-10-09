# Sendgrid

Go through the setup flow to get API_KEY

## Node

utils.js

```js
const sgMail = require("@sendgrid/mail");
sgMail.setApiKey(conf.get("SENDGRID_API_KEY"));
module.exports = {sgMail};
```

router/user.js

```js
const { sgMail } = require("../utils.js");

const msg = {
  to: "jsjfuentesj@gmail.com",
  from: {
    email: "friends.modulo@gmail.com",
    name: "Team Modulo"
  },
  dynamic_template_data: {
    article_link: req.body.url
  },
  template_id: "d-256323a1409f4afc8e1fa85682b248b3"
};
await sgMail.send(msg);
```

