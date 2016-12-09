install
```
mkdir /var/www
cd /var/www
git clone https://github.com/RustJason/xhprof
cd xhprof
git checkout php7
cd extension
phpize
./configure --with-php-config=/usr/bin/php-config
sudo make && sudo make install
```

to php configs
```
mkdir /var/tmp/xhprof

[xhprof]
extension=xhprof.so
xhprof.output_dir="/var/tmp/xhprof"

systemctl restart php7.0-fpm
```

to nginx config
```
location /prof/ {
        root /var/www/xhprof/xhprof_html;
        try_files $uri $uri/ /prof/index.php$is_args$args;

        location ~ (/[a-zA-Z]+\.php) {
            fastcgi_pass  php; //php socket
            fastcgi_index  index.php;
            fastcgi_param SCRIPT_FILENAME $document_root$1;
            include fastcgi_params;
        }
    }
```

in your code
```
if (extension_loaded('xhprof'))
{
    include_once '/var/www/xhprof/xhprof_lib/utils/xhprof_lib.php';
    include_once '/var/www/xhprof/xhprof_lib/utils/xhprof_runs.php';

    xhprof_enable(XHPROF_FLAGS_CPU + XHPROF_FLAGS_MEMORY);
}

...

if (extension_loaded('xhprof')) {
     $profilerNamespace = 'test';
     $xhprofData = xhprof_disable();
     $xhprofRuns = new XHProfRuns_Default();
     $runId = $xhprofRuns->save_run($xhprofData, $profilerNamespace);
}

```