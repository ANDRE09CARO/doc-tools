Copy from
/usr/lib/php/7.0 and change

PROD

```
expose_php = Off

error_reporting = E_ALL
display_errors = Off
display_startup_errors = Off
track_errors = Off
log_errors = On
error_log = /var/log/php_errors.log // cli

mysqlnd.collect_memory_statistics = Off

zend.assertions = -1

opcache.enable_cli=0
opcache.memory_consumption=128      // increase if necessary
opcache.max_accelerated_files=5000  // increase if necessary
opcache.max_wasted_percentage=5
opcache.validate_timestamps=0       // disable autorefresh opcache, just refresh by deployment script

session.use_cookies = 1
session.use_only_cookies = 1
session.cookie_httponly = 1
session.use_strict_mode = 1
session.name = PROJSID              // change

session.lazy_write = 1 // since 7.0.0

//set u need to process files
post_max_size = 20M
upload_max_filesize = 20M
max_file_uploads = 20

memory_limit = 64M  //default to hight im cli can use -1

default_charset = "UTF-8"
date.timezone = UTC
```

DEV
```
error_reporting = E_ALL

display_errors = On
display_startup_errors = On
track_errors = On

memory_limit = 64M
default_charset = "UTF-8"

opcache.validate_timestamps=1

//set u need to process files
post_max_size = 20M
upload_max_filesize = 20M
max_file_uploads = 20
```

Logs
```
//php-fpm.ini - one line logs
error_log = /var/log/php7.0-fpm.log

//pool.conf - multiline logs
catch_workers_output = no
php_admin_value[error_log] = /var/log/php/fpm-php.$pool.error.log

//cli - multiline logs
error_log = /var/log/php/cli-php.error.log

```