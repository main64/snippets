```
##
# You should look at the following URL's in order to grasp a solid understanding
# of Nginx configuration files in order to fully unleash the power of Nginx.
# http://wiki.nginx.org/Pitfalls
# http://wiki.nginx.org/QuickStart
# http://wiki.nginx.org/Configuration
#
# Generally, you will want to move this file somewhere, and start with a clean
# file but keep this around for reference. Or just disable in sites-enabled.
#
# Please see /usr/share/doc/nginx-doc/examples/ for more detailed examples.
##

server {
        listen 80;
        listen [::]:80;

        root /home/vagrant/code/hike/public;
        index index.php index.html index.htm;

        server_name hike.oglocal;

        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }

        #error_page 404 /404.html;

        # redirect server error pages to the static page /50x.html
        #
        #error_page 500 502 503 504 /50x.html;
        #location = /50x.html {
        #       root /usr/share/nginx/html;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        location ~ \.php$ {
           try_files $uri =404;
           fastcgi_split_path_info ^(.+\.php)(/.+)$;
           fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
           fastcgi_index index.php;
           fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
           include fastcgi_params;
        }

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        location ~ /\.ht {
                deny all;
        }
}

```
