# Practica-FlaskGuicorn-JavierGarcia

## 1. Configuraciones Previas de la Máquina

Creamos el repositorio de Github y lo clonamos mediante **git clone**.

Una vez hemos clonado el repositorio, entramos dentro de lo que sería el proyecto y hacemos un **vagrant init debian/bullseye64**, con esto se nos creará de manera automática el **Vagrantfile**, pero nosotros lo vamos a editar de la siguiente manera:

![Vagrantfile](/capturas/1.png)

Con esa edición ya si podemos hacer el vagrant up y el vagrant ssh correspondientes.

![vagrantSsh](/capturas/2.png)

## 2. Instalación de paquetes necesarios

Necesitamos instalar pip, nginx y git, que son los paquetes necesarios para poder realizar esta práctica, mediante un **sudo apt-get install -y python3-pip nginx git**.

![Instalar nginx](/capturas/3.png)

Instalamos pipenv y python-dotenv para gestionar el entorno virtual y las variables mediante un **pip3 install pipenv** y **pip3 install python-dotenv**.

![Instalar pipenv](/capturas/4.png)

Nos va a salir una serie de advertencias sobre el PATH, y nosotros vamos a ejecutar **export PATH=$PATH:/home/vagrant/.local/bin**, lo cual se utiliza para agregar un directorio al PATH del sistema, es decir, para que la terminal pueda encontrar y ejecutar programas que estén dentro de esa carpeta.

![PATH](/capturas/5.png)

## 3. Configuración del Entorno y Pipenv

Una vez instalado todo lo necesario vamos a crear la carpeta del proyecto y a cambiarle los permisos.

![crear](/capturas/6.png)

Ahora editamos el .env del proyecto usando **nano /var/www/app/.env** y lo editamos de la siguiente forma:

![.env](/capturas/7.png)

Ahora vamos a iniciar el entorno mediante un **pipenv shell**.

![iniciar-entorno](/capturas/8.png)

Ahora una vez dentro del entorno instalamos Flask y Gunicorn.

![descargar-flask-guicorn](/capturas/9.png)

## 4. Crear la Aplicación de Prueba

Ahora vamos a crear y editar los archivos Python que nos van a hacer falta para llevar a cabo nuestra aplicación, los cuáles son **application.py** y **wsgi.py**:

![application.py](/capturas/10.png)

![wsgi.py](/capturas/11.png)

Una vez editados estos ficheros vamos a comprobar que funciona, tanto con Flask como con Guicorn.

![PruebaFlask](/capturas/12.png)

![PruebaGuicorn](/capturas/14.png)

![Resolucion](/capturas/13.png)

## 5. Crear el servicio Systemd

Primeramente debemos de salirnos del entorno virtual mediante un **exit**, y posteriormente editamos el fichero **/etc/systemd/system/flask_app.service** y colocamos la ruta de guicorn en el lugar correspondiente.

![FlaskApp](/capturas/15.png)

Una vez editado ponemos el servicio a funcionar

![systemctl](/capturas/16.png)

## 5. Configuración de Nginx

Con el servicio comenzado y funcionando correctamente, configuraremos nginx para que haga proxy inverso, para ello editaremos el archivo **/etc/nginx/sites-available/app.conf** de esta forma:

![proxyInverso](/capturas/17.png)

Una vez editado activamos el sitio y reiniciamos el servicio.

![reinciar-servicio](/capturas/18.png)

## 6. Configuración del Hosts

Ahora en nuestra máquina anfitriona, vamos a editar el fichero **etc/hosts** y añadimos la siguiente linea:

![hosts](/capturas/19.png)

Y comprobamos a través de la URL de nuestro sitio web si funciona.

![comprobacion-url](/capturas/20.png)

## 7. Tarea de Ampliación

Ahora detenemos el servicio, eliminamos la app anterior y hacemos un **git clone** del repositorio que nos has dejado en la página web.

![git-clone](/capturas/21.png)

Una vez clonado, le cambiamos los permisos para poder editarla como queramos.

![chown-chmod](/capturas/22.png)

Entramos de nuevo con el **pipenv shell**.

![pipenv-shell](/capturas/23.png)

Y ahora instalamos las dependencias necesarias.

![dependencias](/capturas/24.png)

Ahora con las dependencias instaladas editamos el fichero **/etc/systemd/system/flask_app.service** de la siguiente forma:

![editar-fichero](/capturas/25.png)

Una vez editado ponemos el servicio de nuevo a funcionar.

![relanzar](/capturas/26.png)

Y una vez puesto en funcionamiento correctamente editamos el fichero **/etc/nginx/sites-available/app.conf** y lo dejamos con el siguiente aspecto:

![sites-available](/capturas/27.png)

y ya por último nos quedaría comprobar que nos sale el formulario correspondiente de Azure.

![comprobacion-azure](/capturas/28.png)

Y con esto habríamos finalizado la práctica.













