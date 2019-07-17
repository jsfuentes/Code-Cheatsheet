# Response

- res.json()
- res.sendFile()
- res.send("Hello");
- res.redirect('/events'); //doesn't work well with react router
- res.render('index');

### Respond with Error

```js
return res.status(400).send({
   message: 'This is an error!'
});

res.status(404).send("Oh uh, something went wrong");

res.status(400);
res.send('None shall pass');

res.send(404)
```