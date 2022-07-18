# AMP

Apache MySQL and PHP 

#### Apache
- Apache Server `sudo apachectl start` then navigate to localhost:80,
- need to restart everytime `sudo apachectl restart`
- `http -v`
- `cd /etc/apache2`
- use emacs to edit httpd.conf
- `cd /Library/WebServer/Documents` has the index.html.en that is run by default and is locked down
- could edit that default folder if you want, but ....


####  Php
- Macs come preinstalled with php and apache
- To just run the php file put `#!/usr/bin/php` at the top of php page, or `#!/usr/local/bin/php -d display_errors=STDOUT` for errors
- Files with extension .php are run through the php processor when run and return a html page
- Put in the preconfigured sites folder for use, navigate with `localhost/~jfuentes/[filename.php]`

#### SQLite
- Also preinstalled
- `sqlite3`
