
## 1. Titulo
Persistencia de Datos en Contenedores Docker con PostgreSQL
## 2. Tiempo de duración
105 minutos
## 3. Fundamentos:
Los contenedores Docker son entornos aislados que permiten ejecutar aplicaciones con sus dependencias. Sin embargo, por defecto, los datos generados en un contenedor no persisten si este se elimina. Esto se debe a que el sistema de archivos de un contenedor es efímero.
#### Persistencia con volúmenes:
Un volumen de Docker es un mecanismo para almacenar datos fuera del ciclo de vida del contenedor. Al vincular un volumen al directorio /var/lib/postgresql/data de PostgreSQL, los datos de la base de datos se guardan en el host, permitiendo su recuperación incluso si el contenedor se destruye 
![image](https://github.com/user-attachments/assets/acdb8e01-549f-40d6-82f6-1897a1e9d884)
 ### Figura 1-1. Arquitectura Docker con/sin Volúmenes

#### PostgreSQL:
Sistema de gestión de bases de datos relacional (RDBMS) que utiliza contenedores para despliegues rápidos. Sin un volumen, los datos se pierden al reiniciar el contenedor.

## 4. Conocimientos previos.
- Comandos básicos de Docker (run, stop, rm, volume).
- Conceptos de bases de datos (creación de tablas, inserción de datos).
- Uso de herramientas de administración como pgAdmin o DBeaver.
- Sintaxis SQL para PostgreSQL.

## 5. Objetivos a alcanzar
1. Demostrar la pérdida de datos en contenedores sin volúmenes.
2. Implementar un volumen Docker para persistencia de datos en PostgreSQL.
3. Validar la recuperación de bases de datos después de eliminar y recrear contenedores.
  
## 6. Equipo necesario:
- Computadora Asus vivibook M1603QA RYZEN 5 16GB 512G
- Cliente de PostgreSQL (psql) o herramienta gráfica (DataGrip).
- Computador con Docker instalado (linux fedora)
- consola  Warp

## 7. Material de apoyo.
   
- Documentación oficial de Docker
- Guía rápida de comandos PostgreSQL
- Tutorial de volúmenes en Docker
-  Guía de la asignatura
  
## 8. Procedimiento
#### Base de datos sin volumen
### Paso 1: Crear el contenedor PostgreSQL (server_db1):
```bash
docker run --name server_db1 -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres
```
### Paso 2: Conectar con un administrador de bases de datos:
- Host: localhost
- Puerto: 5432
- Usuario: postgres
- Contraseña: mysecretpassword
  ![Captura desde 2025-04-18 13-19-04](https://github.com/user-attachments/assets/78534727-0565-440b-883d-0297c38cd658)
   ### Figura 1-2. Conexión a la Base da datos DataGrip

### Paso 3: Crear la base de datos test y la tabla customer:
```bash
CREATE DATABASE test;
\c test;  -- Conectarse a la base de datos test
CREATE TABLE customer (id SERIAL PRIMARY KEY, fullname VARCHAR(100), status VARCHAR(50));
INSERT INTO customer (fullname, status) VALUES ('John Doe', 'active');
```
![Captura desde 2025-04-18 13-04-03](https://github.com/user-attachments/assets/b8e32415-dfa6-4210-9ab4-b314511bd0fb)
 ### Figura 1-3. Creación de la base de datos y tabla.

### Paso 4: Detener y eliminar el contenedor:
```bash
docker stop server_db1
docker rm server_db1
```
### Paso 5: Recrear el contenedor (server_db1):
```bash
docker run --name server_db1 -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres
```
### Paso 6: Verificar que la base de datos test no existe:
Al conectarse nuevamente, la base de datos test y los datos se habrán perdido porque no se usó un volumen.
![Captura desde 2025-04-18 13-05-00](https://github.com/user-attachments/assets/60022351-3b09-4657-af78-38adab75a55e)
 ### Figura 1-4. Base de datos test ya no existente.

#### Base de datos con volumen
### Paso 1: Crear un volumen de Docker:
```bash
docker volume create pgdata
```
### Paso 2: Crear el contenedor PostgreSQL (server_db2) con el volumen:
```bash
docker run --name server_db2 -e POSTGRES_PASSWORD=mysecretpassword -v pgdata:/var/lib/postgresql/data -p 5432:5432 -d postgres
```
### Paso 3: Crear la base de datos test, tabla customer e insertar datos:
```bash
CREATE DATABASE test;
\c test;
CREATE TABLE customer (id SERIAL PRIMARY KEY, fullname VARCHAR(100), status VARCHAR(50));
INSERT INTO customer (fullname, status) VALUES ('Jane Smith', 'active');
```
![Captura desde 2025-04-18 13-30-29](https://github.com/user-attachments/assets/f4540b73-190d-459b-bed2-86e2507c8d7b)
 ### Figura 1-5. Creación de la base de datos y tabla.
### Paso 4: Detener y eliminar el contenedor:
```bash
docker stop server_db2
docker rm server_db2
```
### Paso 5: Recrear el contenedor usando el volumen pgdata:
```bash
docker run --name server_db2 -e POSTGRES_PASSWORD=mysecretpassword -v pgdata:/var/lib/postgresql/data -p 5432:5432 -d postgres
```
### Paso 6:
Al conectarse nuevamente, la base de datos test, la tabla customer y los registros estarán intactos gracias al volumen.
![Captura desde 2025-04-18 13-31-32](https://github.com/user-attachments/assets/54f131aa-d73d-43f6-8ffd-a56184be2b9a)
 ### Figura 1-6 Base de datos intactos usando volumen.

## 9. Resultados esperados:
Los datos de la base de datos se pierden al eliminar el contenedor si no se usan volúmenes.
![Captura desde 2025-04-18 13-06-09](https://github.com/user-attachments/assets/4d27f4f2-ed11-44b6-885d-25456353a20b)
 ### Figura 1-7. Base de datos perdida sin usar volumen.


Los datos se mantienen después de eliminar y recrear el contenedor si se utiliza un volumen.
![Captura desde 2025-04-18 13-31-32](https://github.com/user-attachments/assets/789e82da-1a5b-4416-bd64-c93ca001f50a)
 ### Figura 1-6 Base de datos intactos usando volumen.

 ![Captura desde 2025-04-18 13-46-04](https://github.com/user-attachments/assets/bb6a5dec-1b6b-4506-a1a7-2a47611b10c7)

 ### Figura 1-8. Visualización de warp con todos los comandos utilizados en la práctica.

Al realizar esta práctica, se logró comprobar la persistencia de los datos en contenedores Docker, tanto con como sin volúmenes. En el caso de los contenedores sin volumen, se verificó que los datos, incluyendo la base de datos `test` y la tabla `customer`, se pierden al detener y eliminar el contenedor. Por otro lado, al utilizar volúmenes, se pudo garantizar la persistencia de los datos, ya que, al recrear el contenedor, la base de datos y los registros insertados permanecieron intactos. Además, se obtuvo una comprensión más profunda de cómo Docker maneja los datos y cómo los volúmenes proporcionan una solución efectiva para la conservación de la información.

[Escuchar resumen](https://drive.google.com/file/d/1Nsdre2y7IiibsbP5fIUweoL453xNroD5/view?usp=drive_link) 
Resumen en formato audio


## 10. Bibliografía
 Docker Inc. (2023). Docker Documentation. Recuperado de https://docs.docker.com.

PostgreSQL Global Development Group (2023). PostgreSQL 15 Documentation. Recuperado de https://www.postgresql.org/docs/15/.
