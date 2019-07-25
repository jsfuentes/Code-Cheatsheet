# Cron

Apparently you can schedule a file to run with `cron`  command natively in bash :0 

0 * * * * wget -O - -q -t 1 http://CRON_URL

```php
# +---------------- minute (0 - 59)
# |  +------------- hour (0 - 23)
# |  |  +---------- day of month (1 - 31)
# |  |  |  +------- month (1 - 12)
# |  |  |  |  +---- day of week (0 - 6) (Sunday=0)
# |  |  |  |  |
  *  *  *  *  *  command to be executed
```

If you computer is off when it was supposed to be run, doesn't run it 

`anacrontab` apparently can run these jobs after the fact

## Other cron syntax

```
*    *    *    *    *    *
┬    ┬    ┬    ┬    ┬    ┬
│    │    │    │    │    │
│    │    │    │    │    └ day of week (0-7)(0/7 = Sun)
│    │    │    │    └───── month (1 - 12)
│    │    │    └────────── day of month (1 - 31)
│    │    └─────────────── hour (0 - 23)
│    └──────────────────── minute (0 - 59)
└───────────────────────── second (0 - 59, OPTIONAL)
```



| Operator          | Purpose                                                      | Example                                                      |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| asterisk ( * )    | Specifies all possible values for a field                    | An asterisk in the hour time field is equivalent to “every hour.” |
| question mark (?) | A question mark ( ? ) is allowed in the day-of-month and day-of-week fields. It is used to specify “no specific value,” which is useful when you need to specify something in one of these two fields, but not in the other. | If you want a trigger to fire on a particular day of the month (for example, the 10th), but you don't care what day of the week that is, enter 10 in the day-of-month field, and ? in the day-of-week field. |
| dash ( - )        | Specifies a range of values                                  | 2-5, which is equivalent to 2,3,4,5                          |
| comma ( , )       | Specifies a list of values                                   | 1,3,4,7,8                                                    |
| slash ( / )       | Used to skip a given number of values                        | */3 in the hour time field is equivalent to 0,3,6,9,12,15,18,21. The asterisk ( * ) specifies “every hour,” but the /3 means only the first, fourth, seventh.You can use a number in front of the slash to set the initial value. For example, 2/3 means 2,5,8,11, and so on. |
| L (“last”)        | The L character is allowed for the day-of-month and day-of-week fields.Specifies either the last day of the month, or the last *xxx* day of the month. | The value L in the day-of-month field means “the last day of the month,” which is day 31 for January, or day 28 for February in non-leap years. If you use L in the day-of-week field by itself, it simply means 7 or SAT. But if you use it in the day-of-week field after another value, it means “the last *xxx* day of the month.” For example, 6L means “the last Friday of the month.”*HINT:*When you use the L option, be careful not to specify lists or ranges of values. Doing so causes confusing results. |
| W (“weekday”)     | The W character is allowed for the day-of-month field.Specifies the weekday (Monday-Friday) nearest the given day. | If you specify 15W as the value for the day-of-month field, the meaning is “the nearest weekday to the 15th of the month.” So if the 15th is a Saturday, the trigger fires on Friday the 14th. If the 15th is a Sunday, the trigger fires on Monday the 16th. If the 15th is a Tuesday, it fires on Tuesday the 15th. However, if you specify 1W as the value for day-of-month, and the 1st is a Saturday, the trigger fires on Monday the 3rd, because it does not “jump” over the boundary of a month’s days. The W character can only be specified when the day-of-month is a single day, not a range or list of days.*HINT:*You can combine the L and W characters for the day-of-month expression to yield LW, which translates to “last weekday of the month.” |
| pound sign ( # )  | The pound sign ( # ) character is allowed for the day-of-week field. This character is used to specify “the nth” *xxx* day of the month. | The value of 6#3 in the day-of-week field means the third Friday of the month (day 6 = Friday and #3 = the 3rd one in the month).*Other Examples:* 2#1 specifies the first Monday of the month and 4#5 specifies the fifth Wednesday of the month. However, if you specify #5 and there are fewer than 5 of the given day-of-week in the month, no firing occurs that month. |