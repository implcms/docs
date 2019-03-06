# 服务器配置

```
nginx config

location ~ ^/(?!(applications/.*/assets|system/assets)) {
    fastcgi_pass unix:/dev/shm/php-cgi.sock;
    include fastcgi_params;
    fastcgi_param  SCRIPT_FILENAME  $document_root/index.php;
}
```