# Dates

```javascript
Date() //create Date string
new Date() //create Date object 
```

## Moment.js

### Format Dates

```js
moment().format('MMMM Do YYYY, h:mm:ss a'); // July 5th 2019, 3:09:48 pm
moment().format('dddd');                    // Friday
moment().format("MMM Do YY");               // Jul 5th 19
moment().format('YYYY [escaped] YYYY');     // 2019 escaped 2019
moment().format();                          // 2019-07-05T15:09:48-07:00
                                            // undefined
```

### Relative Time

```js
moment("20111031", "YYYYMMDD").fromNow(); // 8 years ago
moment("20120620", "YYYYMMDD").fromNow(); // 7 years ago
moment().startOf('day').fromNow();        // 15 hours ago
moment().endOf('day').fromNow();          // in 9 hours
moment().startOf('hour').fromNow();       // 10 minutes ago
                                          // undefined
```

### Calendar Time

```js
moment().subtract(10, 'days').calendar(); // 06/25/2019
moment().subtract(6, 'days').calendar();  // Last Saturday at 3:09 PM
moment().subtract(3, 'days').calendar();  // Last Tuesday at 3:09 PM
moment().subtract(1, 'days').calendar();  // Yesterday at 3:09 PM
moment().calendar();                      // Today at 3:09 PM
moment().add(1, 'days').calendar();       // Tomorrow at 3:09 PM
moment().add(3, 'days').calendar();       // Monday at 3:09 PM
moment().add(10, 'days').calendar();      // 07/15/2019
                                          // undefined
```