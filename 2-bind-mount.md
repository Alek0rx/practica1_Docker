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
```
docker run -d --name nginx -P -v C:\Users\josu\Desktop\practicas_const\practica1_Docker\nginx\html:/usr/share/nginx/html nginx:alpine
```

### ¿Qué sucede al ingresar al servidor de nginx?
Al ingresar mediante el navegador se obtiene un código de estado 403 (Forbidden) debido a que no hay archivos en el directorio ../nginx/html del host.

### ¿Qué pasa con el archivo index.html del contenedor?
El archivo index.html que viene por defecto queda sobrescrito por el bind mount.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
El servidor muestra una página web con el template descargado. Esto evidencia la funcionalidad de volumen.

### Eliminar el contenedor
```
docker stop nginx; docker rm nginx
```

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
El servidor muestra la misma página web, debido a que se lo montó en el mismo directorio del host (persistencia de datos).

