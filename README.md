
# docker-php-env
entorno docker con php 7.2 para pruebas

Para clonar el repositorio crear un directorio dentro de las rutas de desarrollo, tipicamente:

     '/var/www/'

para clonar el repositorio en tu entorno local: 

    git clone https://github.com/hemovintage/docker-php-env.git

para levantar la instancia de docker es necesario tener instalado docker y docker-compose 
una vez clonado el repo nos situamos en la carpeta correspondiente al mismo y ejecutamos:

*si queremos levantar docker sin visualizar el output* 

  
    docker-compose up -d 

    
*si queres levantar docker y ver la salida de consola, esto es util para ver warnings, fatals o errores o toda clase de logs, ya que queda en escucha permanente del mismo.* 

    docker-compose up

esto descargará las dependencias del mismo, php 7.2, mysql 5.6, etc., y dejará visible la aplicacion (segun la config) en el puerto 8000 (el cual puede ser cambiado por otro). 

    http://localhost:8000

segun la configuracion declarada en el archivo de nginx: 

> $mainfolder/phpdocker/nginx/nginx.conf

    root /application/public;
        index index.php;
siendo ***/application/public*** el directorio virtual creado dentro del contenedor. 
y de manera exterior ***$mainfolder/phpdocker/public/*** 
lo que modifiques, sea desde dentro del contenedor o por fuera tendrá impacto inmediato en la aplicacion. 

Esta aplicacion tiene configurada una base de datos mysql 5.6 y php 7.2 

## Datos utiles sobre Docker:

Para dar de baja un contenedor con un ctrl+c sobre la escucha del contenedor es suficiente para stopearlo.

Para visualizar los contenedores activos ***'docker ps'*** 

    $ docker ps
    CONTAINER ID        IMAGE                  COMMAND                  CREATED             STATUS              PORTS                    NAMES
    89be16bf7a71        dockerphpenv_php-fpm   "/bin/sh -c /usr/b..."   About an hour ago   Up 3 minutes        9000/tcp                 php-enviroment-for-dev-php-fpm
    8a3bc7f056e0        mysql:5.6              "docker-entrypoint..."   About an hour ago   Up 3 minutes        0.0.0.0:8002->3306/tcp   php-enviroment-for-dev-mysql
    683f3ab24451        nginx:alpine           "nginx -g 'daemon ..."   About an hour ago   Up 3 minutes        0.0.0.0:8000->80/tcp     php-enviroment-for-dev-webserver


El contenedor puede ser accedido por consola a traves de la directiva bash usando el container id.

    $ docker exec -it 683f3ab24451 bash 
por si necesitamos por ejemplo instalar algo nuevo o manipular desde dentro algun aspecto del contenedor. 

para detener la aplicacion con todos sus contenedores bastaría con un stop

    $ docker-compose stop
