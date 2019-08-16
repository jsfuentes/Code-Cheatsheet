# Keyboard Input

There are three types of keyboard events: `keydown`, `keypress`, and `keyup`. For most keys, Gecko dispatches a sequence of key events like this:

1. When the key is first pressed, the `keydown` event is sent.
2. If the key is not a modifier key, the `keypress` event is sent.
3. When the user releases the key, the `keyup` event is sent.

| Key     | `event.key`     | `event.code` |
| :------ | :-------------- | :----------- |
| Z       | `z` (lowercase) | `KeyZ`       |
| Shift+Z | `Z` (uppercase) | `KeyZ`       |