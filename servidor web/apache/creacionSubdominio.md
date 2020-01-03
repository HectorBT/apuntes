## Creación de subdominio en apache
<<<<<<< HEAD
---
### [Volver al readme](../../README.md) 
* [Instalación apache](instalacionApache.md) 
---
=======
>>>>>>> 8333b57881a06459bdf07332ea0db21673e2de0b
en la ruta 
~~~
/etc/apache2/sites-available
~~~
crear un archivo con extencion __.dominio.cl.conf__, luego configurar los datos segun corresponda
~~~
<VirtualHost *:80>
	# The ServerName directive sets the request scheme, hostname and port that
	# the server uses to identify itself. This is used when creating
	# redirection URLs. In the context of virtual hosts, the ServerName
	# specifies what hostname must appear in the request's Host: header to
	# match this virtual host. For the default virtual host (this file) this
	# value is not decisive as it is used as a last resort host regardless.
	# However, you must set it for any further virtual host explicitly.
	#ServerName www.example.com

	ServerAdmin webmaster@dominio.cl
	ServerName subdominio.dominio.cl
	ServerAlias www.subdominio.dominio.cl
	DocumentRoot /var/www/carpetaSubdominio/
    	<Directory "/var/www/carpetaSubdominio/">
        	#Options FollowSymLinks
	        #AllowOverride All

        	#Order allow,deny
	        #Allow from all
	    </Directory>

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
	#Include conf-available/serve-cgi-bin.conf

	#ProxyRequests off
	#ProxyPreserveHost on
	#ProxyPass / http://localhost:23513/
	#ProxyPassReverse / http://localhost:23513/

</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
~~~

habilitar el sitio con el comando
~~~
a2ensite subdominio.dominio.cl.conf
~~~
reiniciar servidor web apache
~~~
service apache2 restart
~~~

#### crear archivo de configuracion en bind dentro de la ruta
~~~
/etc/bind/db.subdominio.dominio.cl
~~~
agregar el nombre del subdominio y reemplasar la direccion ip __192.168.0.1__ por la direccion real del servidor
~~~
$TTL	86400
@	IN	SOA	subdominio.dominio.cl. root.subdominio.dominio.cl. (
			      2		; Serial
			 604800		; Refresh
			  86400		; Retry
			2419200		; Expire
			 86400 )	; Negative Cache TTL
;
@	IN	NS	subdominio.dominio.cl.
@   IN  NS  www.subdominio.dominio.cl.
@	IN	A	192.168.0.1
nssub   IN      A       192.168.0.1
mail    IN      A       192.168.0.1
www     IN      A       192.168.0.1
~~~

reiniciar bind 
~~~
/etc/init.d/bind9 restart
~~~

agregar la zona en el archivo __named.config.local__

~~~
//
// Do any local configuration here
//

// Consider adding the 1918 zones here, if they are not used in your
// organization
//include "/etc/bind/zones.rfc1918";

zone "dominio.cl" {
	type master;
	file "/etc/bind/db.dominio.cl";
};

zone "subdominio.dominio.cl" {
  type master;
  file "/etc/bind/db.subdominio.dominio.cl";
  forwarders { };	
};
~~~
