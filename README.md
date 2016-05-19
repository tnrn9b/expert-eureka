# Installing Zend Framework 2 on Ubuntu 16.04 using Apache2.4
## Background: PHP Apache2 Modules
Make sure you known which version of php you have installed, and that the necessary apache modules are enabled.
To check your php version enter `php -v` at the command-line. The output should resimble this:
```sh
   you@yourmachine:/$  php -v
   PHP 7.0.6-12+donate.sury.org~xenial+4 (cli) ( NTS )
   Copyright (c) 1997-2016 The PHP Group
   Zend Engine v3.0.0, Copyright (c) 1998-2016 Zend Technologies
    with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2016, by Zend Technologies
    with Xdebug v2.4.0, Copyright (c) 2002-2016, by Derick Rethans
```
You don't need to have php7.0 installed. What's important is that php is installed and up to date with the base
requirements issued in the Zend Framework 2 documentation.

In order for php to work with apache you need make sure that you have `libapache2-mod-php` installed. Assuming that
it is installed, check to make sure that the mods are enabled. To do this, enter `cd /etc/apache2/mods-available` and
enter `ls -l | grep php`. If the mods are available, the output should look like this:
```sh
   you@yourmachine:/$ cd /etc/apache2/mods-available
   you@yourmachine:/etc/apache2/mods-available$ ls -l | grep php
   -rw-r--r-- 1 root root  867 May 13 05:03 php7.0.conf
   -rw-r--r-- 1 root root   79 May 13 05:03 php7.0.load
```
Endable the module by entering `sudo a2enmod php7.0` (you need to type the appropriate number for your version) and
restart apache by entering `sudo service apache2 restart`.

## Apache setup

For Apache >= 2.4 on recent releases of Ubuntu (16.04 in particular), there are essentially six steps to setting up a virtual host:

1. Create a .conf file `/etc/apache2/sites-available/zf2.project.conf`.
2. Edit the `ServerName` and `DocumentRoot` in your newly created `zf2.project.conf`
3. Edit the `<Directory /var/www/>` directive in /etc/apache2/apache.conf from `AllowOverride None` to `AllowOverride All`.
4. Enable the Rewrite module `sudo a2enmod rewrite` and `sudo service apache2 restart`.
5. Edit the file /etc/hosts to include your the address `127.0.0.1` and your`ServerName`.
6. Enable the virtual host configuration `sudo a2ensite zf2.project.conf` and `sudo service apache2 restart`.

### Create a .conf file `/etc/apache2/sites-available/zf2.project.conf`.

Here's the easiest way to do this:
   1. Ctrl + Alt + t (to open up a terminal)
   2. sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/zf2.project.conf

### Edit the `ServerName` and `DocumentRoot` in your newly created `zf2.project.conf`

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
### Edit the `<Directory /var/www/>` directive in /etc/apache2/apache.conf from `AllowOverride None` to `AllowOverride All`.

Here's the easiest way to do this:
   1. sudo nano /etc/apache2/apache2.conf
   2. page down until you see `<Directory /var/www/>`
   3. Edit the block so that it looks like this:
	```apache
	<Directory /var/www/>
		Options Indexes FollowSymLinks
		AllowOverride All
		Require all granted
	</Directory>
	```

### Enable the Rewrite module.
    
    Do this by entering `sudo a2enmod rewrite` and `sudo service apache2 restart`.
    
### Edit the file /etc/hosts to include your the address `127.0.0.1` and your`ServerName`.

   Here's the easiest way to do this:
   1. sudo nano /etc/hosts
   2. Add `127.0.0.1       zf2.project.localhost` to the top of the file
      It should look like this:

      ```apache
      127.0.0.1       zf2.project.localhost # This goes at the top of the list
	...
      # The following lines are desirable for IPv6 capable hosts
      ```

### Enable the virtual host configuration

    Do this by entering `sudo a2ensite zf2.project.conf` and `sudo service apache2 restart`.
    
## Test by navigating to zf2.project.localhost in your browser.

