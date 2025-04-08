


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

### Paso 1: Ingresar a Docker 

