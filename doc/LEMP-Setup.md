#Howto install a LEMP stack on Debian Jessie

## Dotdep repository
This repository is needed because it provides php7 and newer nginx builds

	Edit /etc/apt/sources.list and add this lines:
		deb http://packages.dotdeb.org jessie all
		deb-src http://packages.dotdeb.org jessie all
	wget https://www.dotdeb.org/dotdeb.gpg
	sudo apt-key add dotdeb.gpg
	sudo apt update
	



##MariaDB:
	sudo apt install mariadb-server
	mysql_secure_installation
		Enter password
		Change password -> n
		Remove anonymous users -> y
		Disalow root login remotely -> y
		Remove test -> y
		Reload -> y
		
##Nginx:
	sudo apt install nginx
	
##PHP:
	sudo apt install php7.0-fpm php7.0-mysql
	
##Configure PHP:
	Uncomment the line security.limit_extensions in /etc/php/7.0/fpm/pool.d/www.conf and change it to "security.limit_extensions = .php"
	sudo systemctl reload php7.0-fpm.service
	
##Configure Nginx:
	Edit the file /etc/nginx/sites-enabled/default:
	Change the "index" line to
		 "index index.php index.html index.htm;"
	Uncomment and modify the location block so that it reads:
	        "location ~ \.php$ {
                	 include snippets/fastcgi-php.conf;
               		 fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
       		 }"
	 Uncomment the block
	         "location ~ /\.ht {
              	  	deny all;
        	}"
	sudo nginx -t
	sudo systemctl reload nginx

	
	
	
	



