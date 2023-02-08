# Chatwoot

- Very cheap chat with simple design

- $0 a month for up to 1k contacts (can practically include on every site)
- Doesnt include Segment integration so have to add manually, but very easy

## [Add to Website](https://www.chatwoot.com/docs/product/channels/live-chat/create-website-channel)

## [Usage](https://www.chatwoot.com/docs/product/channels/live-chat/sdk/setup)

Remove by default

```js
window.chatwootSettings = {
  hideMessageBubble: false,
  position: "left", // This can be left or right
  locale: "en", // Language to be set
  type: "standard", // [standard, expanded_bubble]
  darkMode: "auto", // [light, auto]
};
```

Then trigger with

```js
window.$chatwoot.toggle("open"); // To open widget
window.$chatwoot.toggle("close"); // To close widget
```

Set user with

```js
window.$chatwoot.setUser("<unique-identifier-key-of-the-user>", {
  email: "<email-address-of-the-user@your-domain.com>",
  name: "<name-of-the-user>",
  avatar_url: "<avatar-url-of-the-user>",
  phone_number: "<phone-number-of-the-user>",
});
```

Errors

```js
window.addEventListener("chatwoot:error", function () {
  // ...
});
```

