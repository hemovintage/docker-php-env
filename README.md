
# docker-php-env
entorno docker con php 7.2 para pruebas

Para clonar el repositorio crear un directorio dentro de las rutas de desarrollo, tipicamente:

     '/var/www/'

para clonar el repositorio en tu entorno local: 

    git clone https://github.com/hemovintage/docker-php-env.git

para levantar la instancia de docker es necesario tener instalado docker y docker-compose 
una vez clonado el repo nos situamos en la carpeta correspondiente al mismo y ejecutamos:

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


