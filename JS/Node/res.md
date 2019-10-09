# Response

- res.json()
- res.sendFile(path.join(__dirname, 'index')); 
  - works best with absolue path
- res.send("Hello");
- res.redirect('/events'); 
  - doesn't work well with react router
- res.render('index');
- res.sendStatus(200);

## Render

To render template files, set view folder and static folder.

Relative to dir you launch node process from

```js
app.set('views', './views'); //this is the default 
app.use(express.static('public'))
app.use('/static', express.static('public'))
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