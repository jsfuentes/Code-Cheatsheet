# Cron

Apparently you can schedule a file to run with cron strings natively in bash :0 

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