# Moment

```javascript
moment().format('MMMM Do YYYY, h:mm:ss a'); // April 28th 2019, 11:22:28 pm
moment().format('dddd');                    // Sunday
moment().format("MMM Do YY");               // Apr 28th 19
moment().format('YYYY [escaped] YYYY');     // 2019 escaped 2019
moment().format();                          // 2019-04-28T23:22:28-07:00
```

## Operations

```javascript
let today = moment();
today.add(config.add_days, 'days');
```

