# expert-eureka

### Apache setup

For Apache >= 2.4 on recent releases of Ubuntu (16.04 in particular), there
are essentially three steps to setting up a virtual host:
	
	1. Create a .conf file /etc/apache2/sites-available/${YOUR_WEBSITE_NAME}.conf,
	   the contents of should be: 

	<VirtualHost *:80>
			ServerName  zf2.project.localhost
			ServerAdmin webmaster@localhost
			DocumentRoot /var/www/ZendSkeletonApplication/public
			ErrorLog ${APACHE_LOG_DIR}/error.log
			CustomLog ${APACHE_LOG_DIR}/access.log combined
	</VirtualHost>

Item *	2. Edit /etc/apache2/apache.conf 
	   In apache.conf, look for:
	
	```apacheconf
	<Directory /var/www/>
		Options Indexes FollowSymLinks
		AllowOverride All
		Require all granted
	</Directory>
	```


	3. Edit the file /etc/hosts
		127.0.0.1       zf2.project.localhost # This goes at the top of the list

```apache
  <Directory /var/www/>
	    Options Indexes FollowSymLinks
	    AllowOverride All
	     Require all granted
  </Directory>
```
