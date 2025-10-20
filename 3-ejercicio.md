## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
```
docker network create net-wp
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/

MySQL (imagen oficial mysql:8) guarda sus datos en: /var/lib/mysql dentro del contenedor.

En el esquema del ejercicio carpeta del contenedor (a) es (/var/lib/mysql)

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?

Antes de ejecutar el contenedor la carpeta esta está vacía (sin archivos ni subcarpetas).

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD

```
docker run -d --name mysql_wp --network net-wp -e MYSQL_ROOT_PASSWORD=rootpass123 -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wp_user -e MYSQL_PASSWORD=wp_pass123 -v "C:\Users\Ricardo\ejercicio3\db:/var/lib/mysql" mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?

Después de que el contenedor arranque y MySQL inicialice la base de datos, en C:\Users\Ricardo\ejercicio3\db aparecerán archivos y carpetas como ibdata1, ib_logfile0, ib_logfile1, carpetas como mysql, performance_schema, wordpress (la base de datos creada) y otros ficheros propios de InnoDB/MySQL.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/

WordPress (imagen oficial) guarda los archivos del sitio en: /var/www/html dentro del contenedor. (La carpeta wp-content/uploads es donde se guardan archivos subidos por usuarios). 
En el esquema del ejercicio la carpeta del contenedor (b) es (/var/www/html.)

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
# COMPLETAR CON EL COMANDO
```
docker run -d --name wordpress_wp --network net-wp -e WORDPRESS_DB_HOST=mysql_wp:3306 -e WORDPRESS_DB_USER=wp_user -e WORDPRESS_DB_PASSWORD=wp_pass123 -e WORDPRESS_DB_NAME=wordpress -p 8080:80 -v "C:\Users\Ricardo\ejercicio3\www:/var/www/html" wordpress:latest
```

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA 
Existen dos opciones: Si se crea los contenedores usando exactamente los mismos mapeos de volumen (C:\Users\Ricardo\ejercicio3\db:/var/lib/mysql y C:\Users\Ricardo\ejercicio3\www:/var/www/html) los datos persisten: la base de datos y los archivos del sitio se mantienen porque están en la carpeta host.
Sin embargo, si se crea el contenedor sin mapear los volúmenes, se perdera la persistencia y el sitio quedará vacío (MySQL inicializará una base de datos nueva vacía).

