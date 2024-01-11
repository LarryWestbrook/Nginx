# Instalación de Nginx en una instancia de AWS.

- Primero que nada actualizamos el sistema

```sh
sudo apt update
sudo apt upgrade
```

- Luego procederemos a instalar Nginx 

```sh
sudo apt install nginx
```
![image](/img/Captura%20desde%202024-01-11%2012-38-07.png)

- Por ultimo accederemos a través de nuestra ip en un navegador web. En mi caso es la Ip publica ya que estoy preprando el servidor web en una instancia de AWS.

```sh
http://tu_ip
```

![image](/img/Captura%20desde%202024-01-11%2012-42-51.png)