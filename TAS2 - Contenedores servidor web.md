


## 1. Título

**Crear y personalizar dos servidores web con Nginx usando DockerDocker Playground)**

## 2. Tiempo de duración

**45 minutos**  

## 3. Fundamentos

Las herramientas de virtualización continua son necesarias para implementar y distribuir aplicaciones en toda la red. Docker es una plataforma para crear, ejecutar y administrar contenedores. Un contenedor es una instancia liviana y portátil que contiene todo lo necesario para una aplicación: código, clientes y configuración.

Nginx es un servidor web de alto rendimiento que también puede actuar como equilibrador de carga y proxy inverso. Se utiliza ampliamente debido a su velocidad, eficiencia y bajos subsidios al consumidor.

En esta practica se utilizó contenedores Docker en el entorno Docker Playground, una herramienta en línea para experimentar con Docker sin instalarlo en un sitio. Con Nginx se creo dos servidores web independientes, cada uno con contenido personalizado.

En la  práctica  se incluyó el uso de los siguientes comandos básicos de Docker:

- `docker run`: para crear y ejecutar contenedores.
- `docker cp`: para copiar archivos entre el host y el contenedor.
- `docker exec`: para ejecutar comandos dentro de un contenedor en ejecución.

A continuación, una representación conceptual del despliegue:

### Figura 1-1. Diagrama de contenedores desplegados en Docker Playground
![image](https://github.com/user-attachments/assets/2dbb91c8-d375-4d66-a0c0-40c7ecc364de)


## 4. Conocimientos previos

Para realizar esta práctica, se  debio tener conocimientos sobre:

- Comandos básicos de Linux (cp, cd, nano, vi, etc.).
- Uso de terminal en sistemas Unix-like.
- Navegación en entornos web.
- Conceptos básicos de redes (puertos, localhost).
- Fundamentos de servidores web.
- Principios de virtualización y contenedores.



## 5. Objetivos a alcanzar

- Implementar contenedores de Nginx en Docker Playground.
- Personalizar el contenido web de cada contenedor mediante archivos HTML.
- Comprender el proceso de despliegue de servicios web en entornos virtualizados.
- Utilizar comandos Docker para manipular archivos dentro de los contenedores.


## 6. Equipo necesario

- Computadora Asus vivibook M1603QA RYZEN 5 16GB 512G
- Conexión a internet.
- Cuenta gratuita en [https://labs.play-with-docker.com](https://labs.play-with-docker.com).
- Navegador web compatible (Chrome, Firefox).
- Docker Playground.

## 7. Material de apoyo

- Documentación oficial de Docker: [https://docs.docker.com](https://docs.docker.com)
- Guía de la asignatura
- Cheat Sheet de comandos Docker
- Videos tutoriales proporcionados por el docente

## 8. Procedimiento

### Paso 1: Ingresar a Docker Playground

Acceder a [https://labs.play-with-docker.com](https://labs.play-with-docker.com) y crear una instancia.


### Paso 2: Crear los contenedores

```bash
docker run -d --name nginx1 -p 8089:80 nginx
docker run -d --name nginx2 -p 8090:80 nginx
```
### Paso 3: Copiar el archivo index.html al host (anfitrión)
```bash
docker cp nginx1:/usr/share/nginx/html/index.html ./index1.html
docker cp nginx2:/usr/share/nginx/html/index.html ./index2.html
```
### Paso 4: Editar los archivos HTML  vi
```bash
vi index1.html
```
```bash
vi index2.html
```
Se borro el contenido utilizando  
```bash 
:%d
 ```
y se reemplazo por:
index1.html – Institucional
```bash
<!DOCTYPE html>
<html>
<head>
  <title>Instituto Tecnológico</title>
</head>
<body>
  <h1>Bienvenido al Instituto Tecnológico Cuenca</h1>
  <p>Formando profesionales para el futuro</p>
</body>
</html>
```
index2.html – Personal

```bash
<!DOCTYPE html>
<html>
<head>
  <title>Perfil Estudiante</title>
</head>
<body>
  <h1>Juan Pérez</h1>
  <p>Estudiante de Ingeniería en Sistemas</p>
</body>
</html>

```
Luego para guardar y salir se coloco:
```bash
:wq
``` 
###  Paso 5: Copiar los archivos editados de regreso al contenedor
```bash
docker cp index1.html nginx1:/usr/share/nginx/html/index.html
docker cp index2.html nginx2:/usr/share/nginx/html/index.html
```
### Paso 6: Ver los resultados en el navegador
En Docker Playground, hacer clic en "Open Port" y escribir el puerto:

Para nginx1: 8089

Para nginx2: 8090

## Resultados Esperados

Al acceder al navegador por los puertos expuestos, se debe visualizar:

Figura 1-2. Página del contenedor nginx1 con contenido institucional

![Captura de pantalla 2025-04-07 181243](https://github.com/user-attachments/assets/6e294e93-85e1-4e97-a06a-78b893d04b60)


Figura 1-3. Página del contenedor nginx2 con contenido personal
![Captura de pantalla 2025-04-07 182342](https://github.com/user-attachments/assets/5e56d1c8-a889-4f96-b511-26899301fe39)

Figura 1-4. Pasos Utilizados en esta práctica 
![Captura de pantalla 2025-04-07 181234](https://github.com/user-attachments/assets/cff5d31c-deca-4e38-85ef-6c1f46301a5a)




Esto indica que los contenedores están funcionando correctamente y se ha logrado la personalización del contenido.


