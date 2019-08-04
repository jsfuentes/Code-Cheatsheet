# Response

- res.json()
- res.sendFile()
- res.send("Hello");
- res.redirect('/events'); //doesn't work well with react router
- res.render('index');

## Render

To render template files, set view folder

```js
app.set('views', './views'); //this is the default 
```

Examples

```javascript
res.render('index', { title: 'Hey', msg: 'Hello!' })
```

### Respond with Error

```js
res.status(400).send({
   message: 'This is an error!'
});

res.status(404).send("Oh uh, something went wrong");

res.status(400);
res.send('None shall pass');

res.send(404)
```