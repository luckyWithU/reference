"# reference" 
https://devanswe.rs/install-secure-phpmyadmin-nginx-ubuntu-20-04/
https://computingforgeeks.com/how-to-install-php-on-ubuntu/
https://techincent.com/how-to-add-ssl-certificate-in-aws-ec2-ubuntu-nginx-server-with-a-custom-domain/

location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri /index.html;
        }

        location /pma_hidden/ {
                alias /usr/share/phpmyadmin/;
                index index.html index.htm index.php;
                auth_basic "Restricted Access";
                auth_basic_user_file /etc/nginx/.htpasswd;

                location ~ ^/pma_hidden(.+\.php)$ {
                alias /usr/share/phpmyadmin$1;
                fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
                fastcgi_param SCRIPT_FILENAME /usr/share/phpmyadmin$1;
                include fastcgi_params;
                fastcgi_intercept_errors on;
                }
        }
