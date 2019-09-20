# yii2-nginx-configuration

## Langkah-langkah konfigurasi nginx untuk yii2 di windows
- Start php cgi

```
path_php>php-cgi.exe -b 127.0.0.1:9000
```  

- Lakukan konfigurasi di file nginx.conf  

```
    server {
        listen       8081;
        server_name  localhost;
		root   html/aplikasi1/web;
		index  index.php index.html index.htm;			
        charset utf-8;

        location / {
			try_files $uri $uri/ /index.php$is_args$args;
        }

		location ~ ^/assets/.*\.php$ {
			deny all;
		}

		location ~ \.php$ {
			include fastcgi_params;
			fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
			fastcgi_pass 127.0.0.1:9000;
			try_files $uri =404;
		}

		location ~* /\. {
			deny all;
		}
	
    }
	
    server {
        listen       8082;
        server_name  localhost;
		root   html/aplikasi2/web;
		index  index.php index.html index.htm;			
        charset utf-8;

        location / {
			try_files $uri $uri/ /index.php$is_args$args;
        }

		location ~ ^/assets/.*\.php$ {
			deny all;
		}

		location ~ \.php$ {
			include fastcgi_params;
			fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
			fastcgi_pass 127.0.0.1:9000;
			try_files $uri =404;
		}

		location ~* /\. {
			deny all;
		}
	
    }	

```

- Jalankan aplikasi nginx
```
path_nginx> nginx.exe
```

- Buka url dan port sesuai konfigurasi nginx, http://localhost:8081 dan http://localhost:8082

## Referensi
https://www.yiiframework.com/doc/guide/2.0/en/start-installation#recommended-nginx-configuration  
https://www.mkyong.com/nginx/nginx-php-on-windows/