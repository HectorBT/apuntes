## Instalación y configuración de Apache2 – Servidor Web Debian 8 Jessie
<<<<<<< HEAD
---
### [Volver al readme](../../README.md) 
* [Crear subdominio](creacionSubdominio.md) 
---
=======
>>>>>>> 8333b57881a06459bdf07332ea0db21673e2de0b
para la instalacion del servidor web apache escribir el siguiente comando
~~~
apt-get install apache2 apache2-mpm-prefork
~~~
El fichero de configuración del software Apache se encuentra en la siguiente ruta:
~~~
etc/apache2/apache2.conf
~~~
 
<<<<<<< HEAD
=======
 para la creacion de un subdominio pinchar [aquí](./instalacionApache.md "creacion de subdominios")
>>>>>>> 8333b57881a06459bdf07332ea0db21673e2de0b
~~~
<VirtualHost *:80>
DocumentRoot /www/example1
ServerName www.example1.com

# Other directives here

</VirtualHost>
~~~
