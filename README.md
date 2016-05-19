# expert-eureka

### Apache setup

For Apache >= 2.4 on recent releases of Ubuntu (16.04 in particular), there
are essentially three steps to setting up a virtual host:
	
	1. Create a .conf file `/etc/apache2/sites-available/zf2.project.conf`.
		Here's the easiest way to do this:
	        1. `Ctrl + Alt + t` (to open up a terminal)
	        2. `sudo cp /etc/apache2/sites-available/default-000.conf /etc/apache2/sites-available/zf2.project.conf`
	2. Edit the `apache ServerName` and `apache DocumentRoot` your newly created `zf2.project.conf`.
	        Here's the easiest way to do this:
		1. 
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
