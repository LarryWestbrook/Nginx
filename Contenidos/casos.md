# Casos prácticos

Ahora procederemos a ver una serie de casos prácticos sobre Nginx.

**a) Versión de Nginx instalado.**

```sh
nginx -v
```
![image](/img/Captura%20desde%202024-01-11%2012-51-12.png)

**b) Ficheros de configuración.**

Los archivos de configuración de Nginx generalmente se encuentran en el directorio /etc/nginx/. El archivo principal de configuración es nginx.conf, pero también puedes encontrar configuraciones específicas para sitios virtuales en el directorio sites-available o en un archivo llamado default o default.conf. 

```sh
sudo nano /etc/nginx/nginx.conf
sudo nano /etc/nginx/sites-available/default
```

![image](/img/Captura%20desde%202024-01-11%2012-54-50.png)

**c) Página web por defecto:**

La página web por defecto de Nginx se encuentra en el directorio de documentos por defecto, que podría ser /var/www/html/. El archivo principal es generalmente index.html.

```sh
sudo nano /var/www/html/index.nginx-debian.html 
```

![image](/img/Captura%20desde%202024-01-11%2012-58-45.png)

Podemos modificar dicho archivo y convertirlo en una pagina web propia.

![image](/img/Captura%20desde%202024-01-11%2013-27-51.png)

![image](/img/Captura%20desde%202024-01-11%2013-29-58.png)

**d) Virtual Hosting:**

Queremos que nuestro servidor web ofrezca balanceo de carga desde https a dos sitios web que tengan también https.

Primero, elimina el archivo de configuración predeterminado de Nginx y crea un nuevo archivo de configuración del balanceador de carga:

```sh
rm -rf /etc/nginx/sites-enabled/default 
nano /etc/nginx/conf.d/load-balancing.conf
```

Añade las siguientes líneas:

```sh
upstream backend {
        server 192.168.10.11;
        server 192.168.10.12;
    }
	
    server {
        listen      80;
        server_name loadbalancing.example.com;

        location / {
	        proxy_redirect      off;
	        proxy_set_header    X-Real-IP $remote_addr;
	        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
	        proxy_set_header    Host $http_host;
		proxy_pass http://backend;
	}
}
```

Guarda y cierra el archivo cuando hayas terminado.

Inserta las siguientes líneas si quieres usar el método Least_conn:

```sh
upstream backend {
        least_conn;
        server 192.168.10.11;
        server 192.168.10.12;
    }
```

Inserta las siguientes líneas si quieres usar el método Ip_hash:

```sh
upstream backend {
	ip_hash;
        server 192.168.10.11;
        server 192.168.10.12;
    }
```

Guarda y cierra el archivo y luego verifica Nginx para detectar cualquier error de sintaxis con el siguiente comando:

```sh 
nginx -t
```

Deberías obtener el siguiente resultado:

![image](/img/Captura%20desde%202024-01-11%2014-13-10.png)

Para terminar, reinicia el servicio Nginx para aplicar los cambios:

```sh
systemctl restart nginx
```

- Verifica el Balanceo de Carga

Ahora abre tu navegador web y accede al servidor de equilibrio de carga utilizando la URL http://loadbalancing.example.com. Serás redirigido al servidor de aplicaciones1: