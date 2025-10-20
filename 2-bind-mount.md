# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
# COMPLETAR CON EL COMANDO
```
docker run -d --name mynginx -p 8080:80 -v "C:\Users\Ricardo\Documents\nginx\html:/usr/share/nginx/html:ro" nginx:alpine
```

### ¿Qué sucede al ingresar al servidor de nginx?

Al colocar la dirección del localhost y el puerto en mi barra de busqueda de mi navegador ingreso normalmente al html que puse al inicio de la práctica, como se muestra en la imagen.
<img width="1916" height="1142" alt="image" src="https://github.com/user-attachments/assets/9c6240bf-ffea-4a3c-aa52-6e2658d16063" />


### ¿Qué pasa con el archivo index.html del contenedor?

El index.html que viene dentro de la imagen no es eliminado de la imagen, pero queda oculto por el bind mount: al montar la carpeta del host sobre /usr/share/nginx/html, el contenido original de esa ruta en el contenedor no es visible mientras exista el montaje.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?

Al recargar http://localhost:8080 se muestra el template completo (HTML, CSS, imágenes) servido por nginx, porque ahora en la carpeta del host hay archivos del template que el servidor web entrega. 

<img width="1877" height="1125" alt="image" src="https://github.com/user-attachments/assets/9d62a5f5-7efd-4d5f-97e5-2b4ef6e917e5" />


### Eliminar el contenedor

```
docker rm -f mynginx
```

<img width="471" height="64" alt="image" src="https://github.com/user-attachments/assets/06278a61-351b-47fb-9ec5-757d593d382e" />


### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?

Al crear otro contenedor con el mismo bind mount, nginx volverá a servir los mismos archivos que están en la carpeta del host (~/nginx/html). Es decir: El contenido del host perdura aunque elimines el contenedor.


