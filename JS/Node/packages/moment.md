# Moment

### Creation

```js
moment(String);
moment("12-25-1995", "MM-DD-YYYY"); //pass format of string 
```

### Formatting

```javascript
//This one is the best because string sorting works
moment().format(); // 2019-04-28T23:22:28-07:00

moment().format('MMMM Do YYYY, h:mm:ss a'); 
// April 28th 2019, 11:22:28 pm
moment().format('dddd'); // Sunday
moment().format("MMM Do YY"); // Apr 28th 19
moment().format('YYYY [escaped] YYYY');     
// 2019 escaped 2019
```

### Operations

```javascript
let today = moment();
today.add(config.add_days, 'days');
```

##### Get And Setters

Leave empty to get and give Number/String to set

```js
moment().month();//return 0-11 which is Jan-Dec
moment().day();//return 0-6 which is Sun-Sat
moment().date(); //return 1-31 for day of month
```

### Plugins

#### [moment-business-days](https://github.com/kalmecak/moment-business-days)

Only work with business days adding fts like isHoliday and businessDiff to moment

#### Formatting Tables

| Input      | Example          | Description                                            |
| :--------- | :--------------- | :----------------------------------------------------- |
| `YYYY`     | `2014`           | 4 or 2 digit year                                      |
| `YY`       | `14`             | 2 digit year                                           |
| `Y`        | `-25`            | Year with any number of digits and sign                |
| `Q`        | `1..4`           | Quarter of year. Sets month to first month in quarter. |
| `M MM`     | `1..12`          | Month number                                           |
| `MMM MMMM` | `Jan..December`  | Month name in locale set by `moment.locale()`          |
| `D DD`     | `1..31`          | Day of month                                           |
| `Do`       | `1st..31st`      | Day of month with ordinal                              |
| `DDD DDDD` | `1..365`         | Day of year                                            |
| `X`        | `1410715640.579` | Unix timestamp                                         |
| `x`        | `1410715640579`  | Unix ms timestamp                                      |

| Input      | Example        | Description                                 |
| :--------- | :------------- | :------------------------------------------ |
| `gggg`     | `2014`         | Locale 4 digit week year                    |
| `gg`       | `14`           | Locale 2 digit week year                    |
| `w ww`     | `1..53`        | Locale week of year                         |
| `e`        | `0..6`         | Locale day of week                          |
| `ddd dddd` | `Mon...Sunday` | Day name in locale set by `moment.locale()` |
| `GGGG`     | `2014`         | ISO 4 digit week year                       |
| `GG`       | `14`           | ISO 2 digit week year                       |
| `W WW`     | `1..53`        | ISO week of year                            |
| `E`        | `1..7`         | ISO day of week                             |

| Input      | Example  | Description                                                  |
| :--------- | :------- | :----------------------------------------------------------- |
| `H HH`     | `0..23`  | Hours (24 hour time)                                         |
| `h hh`     | `1..12`  | Hours (12 hour time used with `a A`.)                        |
| `k kk`     | `1..24`  | Hours (24 hour time from 1 to 24)                            |
| `a A`      | `am pm`  | Post or ante meridiem (Note the one character `a p` are also considered valid) |
| `m mm`     | `0..59`  | Minutes                                                      |
| `s ss`     | `0..59`  | Seconds                                                      |
| `S SS SSS` | `0..999` | Fractional seconds                                           |
| `Z ZZ`     | `+12:00` | Offset from UTC as `+-HH:mm`, `+-HHmm`, or `Z`               |