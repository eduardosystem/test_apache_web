# test_apache_web
Aplicacion simple de un servidor apache en un contenedor docker.

MANTENIMIENTO Newstar Corporation

EJECUTAR : antes de crear una imagen si desea alguna configuración que debe estar presente en la imagen. Dentro de la imagen necesitamos instalar la imagen del servidor web Apache, el comando para instalar esa imagen es
EJECUTAR yum –y instalar httpd

COPIAR : este comando se utiliza para copiar un archivo del sistema operativo del host al contenedor de Docker
COPY index.html / var / www / html

EXPOSE : este comando se utiliza para especificar el número de puerto en el que el contenedor ejecuta su proceso. Cualquiera puede venir de afuera y conectarse a este puerto. El servidor web Apache se inicia en el puerto 80 de forma predeterminada, por eso necesitamos exponer el contenedor en el puerto 80.
EXPOSE 80

CMD : para ejecutar un comando tan pronto como se inicie el contenedor. El comando CMD es diferente de RUN porque RUN se usa al momento de construir una imagen y CMD se usa para ejecutar el comando cuando se inicia el contenedor.
/ usr / sbin / httpd: este comando se utiliza para iniciar el servidor web
-DFOREGROUND: este no es un comando acoplable, es un argumento del servidor http que se utiliza para ejecutar el servidor web en segundo plano. Si no usamos este argumento, el servidor se iniciará y luego se detendrá.
CMD ["/ usr / sbin / httpd", "-D", "FOREGROUND"]

''
# CREAR IMAGEN DOCKERFILE
''

- 	Creamos una carpeta: 
      ```
      test_apache_web
      ```

- 	Creamos el archivo: index.html
      ```
      <!DOCTYPE html>
      <html>
      <body>
      <h1>App demo apache, docker</h1>
      </h2>https://apache.com</h2>
      </body>
      </html>
      ```

- 	Creamos el archivo: Dockerfile
      ```
      FROM centos:latest
      MAINTAINER EduardoRuiz
      RUN yum -y install httpd
      COPY index.html /var/www/html
      CMD ["/usr/sbin/httpd","-D","FOREGROUND"]
      EXPOSE 80
      ```
- 	Compilamos o creamos la imagen: desde la carpeta raiz
      ```
      $ docker build ./test_apache_web/ -t servidorweb:v1
      ```
      
- 	Ejecutamos la imagen
      ```
      $ docker run -dit -p 1234:8080 servidorweb:v1
      ```
