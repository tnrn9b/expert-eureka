# expert-eureka

### Apache setup

For Apache >= 2.4 on recent releases of Ubuntu (16.04 in particular), there
are essentially three steps to setting up a virtual host:
	
1. Create a .conf file `/etc/apache2/sites-available/zf2.project.conf`.
   Here's the easiest way to do this:
   1. Ctrl + Alt + t (to open up a terminal)
   2. sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/zf2.project.conf

2. Edit the `ServerName` and `DocumentRoot` in your newly created `zf2.project.conf`
   changing them to: 
```apache 
	...
	Servername zf2.project.localhost
	...
	DocumentRoot /var/www/{NAME_OF_YOUR_ZEND_PROJECT_DIR}/public
```	
   Here's the easiest way to do this (using nano as an editor):
	1. sudo nano /etc/apache2/sites-available/zf2.project.conf
	2. make the changes to the lines described above, removing the '#' from
	   in front of the `ServerName`.
	   It should look something like this:
```apache
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        ServerName zf2.project.localhost
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/{NAME_OF_YOUR_ZEND_PROJECT_DIR}/public

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        # Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```




	



	2. Edit /etc/apache2/apache.conf 
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
