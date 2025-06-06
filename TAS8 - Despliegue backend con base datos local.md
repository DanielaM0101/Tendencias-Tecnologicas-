

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


<div align="center">
  <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 005427.png" width="800" />
  <br>
  Figura 1.  Arquitectura básica de contenedores Docker y servicios.
</div>



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


**Paso 2:** Crear los Archivos Necesarios
```bash
nano docker-compose.yml
  ```

**Paso 3:** Crear y configurar el archivo `docker-compose.yml` con los servicios necesarios.
> **Figura 8-3-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-01 233240.png" alt="drawing" width="800"/>


**Paso 4:** Definir las variables de entorno en un archivo `.env`.
> **Figura 8-4-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-01 232921.png" alt="drawing" width="800"/>
 

**Paso 5:** Crear un `Dockerfile` con estrategia de construcción multi-stage para la aplicación backend.
> **Figura 8-5-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-01 235132.png" alt="drawing" width="800"/>
 

**Paso 6:** Construir e iniciar los contenedores usando Docker Compose.
> **Figura 8-6-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-01 235647.png" alt="drawing" width="800"/>
 
> **Figura 8-6-2.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 000423.png" alt="drawing" width="800"/>

**Paso 7:** Acceder a pgAdmin desde el navegador y crear un nuevo servidor con los datos de conexión.
> **Figura 8-7-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 005716.png" alt="drawing" width="800"/>
 
> **Figura 8-7-2.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001104.png" alt="drawing" width="800"/>
 
> **Figura 8-7-3.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001125.png" alt="drawing" width="800"/>
 
> **Figura 8-7-4.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001135.png" alt="drawing" width="800"/>
 
**Paso 8:** Verificar la conexión de pgAdmin a PostgreSQL.
> **Figura 8-8-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001831.png" alt="drawing" width="800"/>


**Paso 9:** Comprobar que la aplicación backend se conecta correctamente a la base de datos.
> **Figura 9-9-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001250.png" alt="drawing" width="800"/>
 

**Paso 10:** Crear y configurar el archivo `CorsConfig.kt` para habilitar CORS en el backend.
> **Figura 8-10-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 001935.png" alt="drawing" width="800"/>
 

**Paso 11:** Probar el endpoint `/users` desde el navegador o herramienta de prueba de APIs.
> **Figura 8-11-1.**
 <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 004720.png" alt="drawing" width="800"/>

> **Figura 8-11-2.**
  <img src="./../../Tools/Photos/2do-Semana-8/Captura de pantalla 2025-06-02 012126.png" alt="drawing" width="800"/>


## 9. Resultados esperados  

Al finalizar la práctica, se espera que los siguientes resultados sean evidentes:  
- Contenedores de PostgreSQL, pgAdmin y backend corriendo sin errores.  
- Persistencia de datos garantizada mediante volúmenes.  
- Acceso a pgAdmin vía navegador y conexión exitosa a la base de datos.  
- Endpoint `/users` respondiendo con una lista en formato JSON de usuarios almacenados en la base de datos.  
- Imagen Docker optimizada y contenedores fácilmente replicables.  

Ejemplo de respuesta en navegador para `http://localhost:8081/users`:

```json
[
  {
    "id": 1,
    "username": "jdoe",
    "email": "jdoe@example.com",
    "passwordHash": "3c59dc048e8850243be8079a5c74d079",
    "isActive": "t",
    "createdAt": "2025-06-02 05:04:05.766085"
  },
  ...
]
```

  ## 🔊 Audio Explicativo de la practica.
https://drive.google.com/file/d/10UL3iFNJ-jRgvvaaBtAelhagdXRXs97M/view?usp=sharing

## 10. Bibliografía

- Docker Inc. (s.f.). Docker Documentation. Recuperado de https://docs.docker.com/
- González, F. (2023). Guía de implementación de entornos web con contenedores. Universidad Sudamericana.
- dpage. (2024). phpMyAdmin documentation. Recuperado de https://www.phpmyadmin.net/docs/
