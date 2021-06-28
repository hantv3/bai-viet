`server {
  listen 80;
  listen [::]:80;
  server_name _;
  root /var/www/;
  index index.php index.html index.htm;

  location / {
    try_files $uri $uri/ /index.php;
  }

  location ~ .php$ {
        try_files $uri $uri/ =404;
        fastcgi_split_path_info ^(.+.php)(/.+)$;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
        fastcgi_intercept_errors on;

        if (-f $request_filename)
        {
            fastcgi_pass 0.0.0.0:9000;
        }
    }

  location ~* .(jpg|jpeg|gif|png|webp|svg|woff|woff2|ttf|css|js|ico|xml)$ {
       access_log        off;
       log_not_found     off;
       expires           360d;
  }

  location ~ /.ht {
      access_log off;
      log_not_found off;
      deny all;
  }
}`
