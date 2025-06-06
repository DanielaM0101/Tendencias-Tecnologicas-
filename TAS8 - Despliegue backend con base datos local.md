

## 1. Título  
**Automatizar el despliegue de una aplicación backend utilizando Docker y Docker Compose, incluyendo la base de datos PostgreSQL y su panel de administración (pgAdmin), todo dentro de un entorno local.**

## 2. Tiempo de duración  
**120 minutos (incluyendo solución de problemas)**  

## 3. Fundamentos
Esta práctica demostró la implementación de una arquitectura de contenedores para aplicaciones backend, utilizando:

- Docker Compose para orquestación de servicios
- PostgreSQL como sistema de base de datos relacional
- pgAdmin para administración visual de la base de datos
- Spring Boot como framework backend
- Se aplicaron conceptos clave de:
- Virtualización ligera con contenedores
- Persistencia de datos con volúmenes Docker
- Comunicación inter-contenedores mediante redes Docker
- Configuración mediante variables de entorno


![imagen](https://github.com/user-attachments/assets/1b893d1f-e92e-4d74-b5ed-61df7a184e1d)



---

## 4. Conocimientos previos  
- Administración básica de contenedores Docker
- Configuración de servicios en docker-compose.yml
- Manejo de variables de entorno
-  Conceptos de redes y puertos en Docker
- Configuración básica de PostgreSQL

## 5. Objetivos a alcanzar  
- Implementar servicios de PostgreSQL y pgAdmin garantizando su persistencia y conectividad.
- Diseñar una imagen optimizada para la aplicación backend utilizando construcciones en varias etapas (multi-stage builds).
- Configurar adecuadamente las variables de entorno y las conexiones entre los diferentes contenedores.
- Validar el correcto funcionamiento de la API mediante pruebas de sus endpoints.
- Automatizar el despliegue de la aplicación backend empleando Docker y Docker Compose.



## 6. Equipo necesario  
- Computadora Asus Vivibook M1603QA (Ryzen 5, 16GB RAM)
- Docker Engine 24.0.7
- Docker Compose v2.23.0
- Sistema operativo Linux (Fedora 41)  

## 7. Material de apoyo  
- Guía de la asignatura y material proporcionado por el profesor.  
- Repositorio base del proyecto: https://github.com/maguaman2/tendencias-mar22-security.git  
- Documentación oficial de Docker: https://docs.docker.com/  
- Documentación de PostgreSQL: https://www.postgresql.org/docs/  


## 8. Procedimiento  

**Paso 1:** Clonar el repositorio base desde GitHub.
```bash
git clone https://github.com/maguaman2/tendencias-mar22-security.git
cd tendencias-mar22-security
  ```


**Paso 2:** Crear y configurar el archivo `docker-compose.yml` con los servicios necesarios.

```bash
nano docker-compose.yml
  ```
![Captura desde 2025-06-05 20-42-22](https://github.com/user-attachments/assets/9b52f385-361a-4a26-9b54-a98383152e74)


**Paso 3:** Definir las variables de entorno en un archivo `.env`.
```bash
nano .env
  ```
![imagen](https://github.com/user-attachments/assets/4bf2fe67-afec-4f1a-9f7e-1c4048398e9c)


**Paso 5:** Crear un `Dockerfile` con estrategia de construcción multi-stage para la aplicación backend.
```bash
nano Dockerfile
  ```
![imagen](https://github.com/user-attachments/assets/47803b57-1495-4ae2-ab24-64935302c3d7)


**Paso 6:** Construir e iniciar los contenedores usando Docker Compose.
```bash
docker-compose up --build
  ```
![imagen](https://github.com/user-attachments/assets/e6a60f28-7322-4518-a6db-0635cca658f4)

**Paso 7:** Acceder a pgAdmin desde el navegador y crear un nuevo servidor con los datos de conexión.

![Captura desde 2025-06-05 20-09-45](https://github.com/user-attachments/assets/beb8f188-71a5-4efb-916c-3dc0932fd9e5)
![Captura desde 2025-06-05 19-24-27](https://github.com/user-attachments/assets/606c8ebf-ca7b-48a8-a349-ea01c00fc1ee)
![Captura desde 2025-06-05 20-10-38](https://github.com/user-attachments/assets/c7049813-e0ae-4c3c-b386-a5717c370d0e)
![Captura desde 2025-06-05 20-14-36](https://github.com/user-attachments/assets/12fd4bd1-a99b-4cbc-9b76-f6d83a0c0d64)



**Paso 7:** Crear y configurar el archivo `CorsConfig.kt` para habilitar CORS en el backend.
![imagen](https://github.com/user-attachments/assets/168e6d64-8b96-48d3-ae10-5eeacf9208d8)


**Paso 11:** Probar el endpoint `/users` desde el navegador o herramienta de prueba de APIs.
![Captura desde 2025-06-05 20-20-18](https://github.com/user-attachments/assets/740e38f6-8e83-4fc3-864b-c069e4bab6cc)

## 9. Resultados esperados  
Al completar la práctica, deberían ser visibles los siguientes resultados:
- Los contenedores de PostgreSQL, pgAdmin y backend funcionando sin fallos.
- La conservación de datos asegurada mediante el uso de volúmenes.
- Poder acceder a pgAdmin a través del navegador y establecer una conexión exitosa con la base de datos.
- El endpoint /users devolviendo una lista en formato JSON con los usuarios almacenados.
- Una imagen Docker optimizada y contenedores que puedan ser reproducidos de manera sencilla.


 

## 10. Bibliografía
- González, F. (2023). Guía de implementación de entornos web con contenedores. Universidad Sudamericana.
- Docker Inc. (s.f.). Docker Documentation. Recuperado de https://docs.docker.com/
- dpage. (2024). phpMyAdmin documentation. Recuperado de https://www.phpmyadmin.net/docs/


