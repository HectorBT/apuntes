## Instalación y configuración de Apache2 – Servidor Web Debian 8 Jessie
---
### [Volver al readme](../../README.md) 
* [Crear subdominio](creacionSubdominio.md) 
---
para la instalacion del servidor web apache escribir el siguiente comando
~~~
apt-get install apache2 apache2-mpm-prefork
~~~
El fichero de configuración del software Apache se encuentra en la siguiente ruta:
~~~
etc/apache2/apache2.conf
~~~
 
~~~
<VirtualHost *:80>
DocumentRoot /www/example1
ServerName www.example1.com

# Other directives here

</VirtualHost>
~~~
