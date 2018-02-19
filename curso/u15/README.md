# Control de acceso. Autorización

El control de acceso, hace referencia a todos los medios que proporcionan una forma de controlar el acceso a cualquier recurso. La directiva [`Require`](https://httpd.apache.org/docs/2.4/es/mod/mod_authz_core.html#require) proporciona una variedad de diferentes maneras de permitir o denegar el acceso a los recursos. Además puede ser usada junto con las directivas: [`RequireAll`](https://httpd.apache.org/docs/2.4/es/mod/mod_authz_core.html#requireall), [`RequireAny`](https://httpd.apache.org/docs/2.4/es/mod/mod_authz_core.html#requireany), y [`RequireNone`](https://httpd.apache.org/docs/2.4/es/mod/mod_authz_core.html#requirenone), estos requerimientos pueden ser combinados de forma compleja y arbitraria, para cumplir cualquiera que sean tus políticas de acceso.

## Directiva Require

Podemos controlar el acceso a cualquier recurso o conjunto de recurso, por ejemplo usando una directiva `Directory`, con `Requiere` usando algunas de estas opciones:

* `Require all granted`: El acceso es permitido incondicionalmente.
* `Require all denied`: El acceso es denegado incondicionalmente.
* `Require user userid [userid] ...`: El acceso es permitido sólo si los usuarios indicados se han autentificado.
* `Require group group-name [group-name] ...`: El acceso es permitido sólo a los grupos de usuarios especificados.
* `Require valid-user`: El acceso es permitido a los usuarios váilidos.
* `Require ip 10 172.20 192.168.2`: El acceso es permitido si el acceso se hace desde el conjunto de direcciones especificadas.

En versiones anteriores de Apache se utilizaban otras directivas para controlar el acceso: [`Allow`](https://httpd.apache.org/docs/2.4/es/mod/mod_access_compat.html#allow), [`Deny`](https://httpd.apache.org/docs/2.4/es/mod/mod_access_compat.html#deny), y [`Order`](https://httpd.apache.org/docs/2.4/es/mod/mod_access_compat.html#order), están obsoletas y serán quitadas en futuras versiones.

Por ejemplo en la versión Apache 2.2 podemos encontrar esta configuración:

	<Directory "/var/www">
		Order allow,deny
		Allow from all
	</Directory>

En Apache 2.4 quedaría:

	<Directory "/var/www">
		Require all granted
	</Directory>

Otro ejemplo, por ejemplo para no permitir el acceso  a fichero `.htaccess`, podíamos encontrar en Apache 2.2:

	<FilesMatch "^\.ht">
   		Order allow,deny
   		Deny from all
	</FilesMatch>

En Apache 2.4 quedaría:

	<FilesMatch "^\.ht">
   		Require all denied
    </FilesMatch>

El uso de las directivas [`RequireAll`](https://httpd.apache.org/docs/2.4/es/mod/mod_authz_core.html#requireall), [`RequireAny`](https://httpd.apache.org/docs/2.4/es/mod/mod_authz_core.html#requireany), y [`RequireNone`](https://httpd.apache.org/docs/2.4/es/mod/mod_authz_core.html#requirenone) la estudiaremos en una unidad posterior.