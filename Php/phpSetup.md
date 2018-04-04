# Apache Setup
On Mac, apache and php come preinstalled
Setup is still needed though

1. To use your own folder, search for `userdir` in `/etc/apache2/httpd.conf` and uncomment the loading of the userdir_ module and uncomment the line including a conf in extra directory
2. then edit the file including `/etc/apache2/extra/http-userdir.conf` and uncomment include the line for `/private/etc/apache2/users/*.conf`
3. `cd /etc/apache2/users` and `sudo emacs [homedirectory name].conf`
```
<Directory "[path to diectory name]">
  Options Indexes MultiViews
  AllowOverride None
  Require all granted
</Directory>
```
4. Finally, go to `localhost/~[name]`

# Apache with Php

1. In `/etc/apache2/httpd.conf` search for Addhandler and add `AddHandler php7-script php` which means php extensions will be handled
2. Then search for php and uncomment the php load module
3. In `cd /private/etc`, `sudo cp php.ini.default php.ini` and finally open the `php.ini` file
4. In the file, find the real display_errors(prob second) and turn from Off to On
5. Finally, restart sever and
