

## 1. Título

**WordPress con Docker**

## 2. Tiempo de duración

**60minutos**  

## 3. Fundamentos

Los contenedores Docker permiten empaquetar aplicaciones y sus dependencias en entornos aislados. Sin embargo, por defecto, los datos generados dentro de un contenedor se pierden al eliminarlo. Para solucionar esto, Docker ofrece:

Volúmenes: Mecanismo para almacenar datos de forma persistente en el host.

Redes: Permiten la comunicación segura entre contenedores.

En este informe, se implementa un sitio WordPress con:

MySQL: Base de datos que almacena el contenido de WordPress.

phpMyAdmin: Interfaz gráfica para administrar MySQL.

WordPress: CMS (Sistema de Gestión de Contenidos) que utiliza MySQL para guardar datos.

### Figura 1-1. Arquitectura de WordPress con Docker
![image](https://github.com/user-attachments/assets/e6385342-d90d-4c72-8cee-034c7fc550b2)



## 4. Conocimientos previos

- Comandos básicos de Docker (run, stop, rm, volume, network).

- Conceptos de bases de datos (usuarios, contraseñas, permisos).

- Uso de terminal en Fedora.


## 5. Objetivos a alcanzar

- Crear una red Docker para conectar contenedores.

- Implementar volúmenes para persistencia de datos en WordPress y MySQL.

- Configurar WordPress con MySQL y phpMyAdmin.

- Verificar la persistencia de datos al reiniciar contenedores.


## 6. Equipo necesario

- Computadora Asus vivibook M1603QA RYZEN 5 16GB 512G   fedora  Docker instalado.
- Conexión a internet.
- Navegador web compatible (Chrome, Firefox).
- Terminal: Warp



## 7. Material de apoyo

- Guía de la asignatura
- Documentación oficial de Docker
- Documentación de WordPress en Docker Hub
- Guía de volúmenes en Docker

## 8. Procedimiento

### Paso 1: Instalar Docker en Fedora
```bash
sudo dnf update
sudo dnf install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
newgrp docker  # Refrescar grupos sin cerrar sesión
```

### Paso 2: Crear una red Docker

```bash
docker network create wp_network
```
### Paso 3:  Crear volúmenes para persistencia
```bash
docker volume create wp_data
docker volume create mysql_data
```
### Paso 4: Desplegar MySQL
```bash
docker run -d --name mysql_db \
  --network wp_network \
  -v mysql_data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=123456 \
  -e MYSQL_DATABASE=wordpress \
  mysql:latest
```


###  Paso 5: Desplegar phpMyAdmin
```bash
docker run -d --name phpmyadmin \
  --network wp_network \
  -e PMA_HOST=mysql_db \
  -p 8080:80 \
  phpmyadmin:latest
```
### Paso 6: Desplegar WordPress
```bash
docker run -d --name wordpress \
  --network wp_network \
  -v wp_data:/var/www/html \
  -e WORDPRESS_DB_HOST=mysql_db \
  -e WORDPRESS_DB_USER=root \
  -e WORDPRESS_DB_PASSWORD=123456 \
  -e WORDPRESS_DB_NAME=wordpress \
  -p 80:80 \
  wordpress:latest
```
### Paso 7: Paso 7: Verificar funcionamiento
WordPress: Abrir http://localhost en el navegador.

phpMyAdmin: Acceder a http://localhost:8080 (usuario: root, contraseña: 123456).

## Resultados Esperados

Al acceder a los puertos expuestos, se obtuvieron los siguientes resultados:
![image](https://github.com/user-attachments/assets/35c57b04-0079-4b38-ab86-584548ad760d)

*Figura 1-2. WordPress (http://localhost:80)

- Se visualizó correctamente el asistente de instalación inicial de WordPress (pantalla de selección de idioma)

- Tras completar la instalación, se mostró el escritorio administrativo (/wp-admin)

- El sitio principal mostraba el tema por defecto "Twenty Twenty-Three"



- Pantalla de login accesible (usuario: root, contraseña: 123456)

- Al ingresar, se visualizó la base de datos "wordpress" creada automáticamente

- Las tablas de WordPress (wp_posts, wp_users, etc.) eran visibles tras la instalación
  ![image](https://github.com/user-attachments/assets/f5bdd4f7-4fc6-413e-b0f4-5fc5f9f6caa8)


*Figura 1-3. phpMyAdmin mostrando la base de datos de WordPress phpMyAdmin (http://localhost:8080)*


![image](https://github.com/user-attachments/assets/f9e6baa4-fe32-47db-aa6d-b9b9a4fda3d5)

*Figura 1-4.Diagrama de los contenedores con los puertos utilizados.*

| Componente           | Resultado Esperado                                               |
|----------------------|------------------------------------------------------------------|
| Red wordpress_net   | Los contenedores pueden comunicarse entre sí.                   |
| Volumen vol_mysql   | Los datos de MySQL persisten tras reinicios.                     |
| Volumen vol_wordpress | Los archivos de WordPress no se pierden.                        |
| phpMyAdmin          | Acceso a la base de datos sin errores.                            |

*Table 1.1 Resultados.

![image](https://github.com/user-attachments/assets/2449de06-8b97-40ff-bd81-81a96c412f4b)

*Figura 1-5 History de los comandos utilizados*

[Escuchar resumen](https://drive.google.com/file/d/1RKVDsjKgqDQZcM-JOKzv5_sYbcoyI_dE/view?usp=sharing)
Resumen en formato audio
 
 
## Bibliografia 
Dock, M. (2023, 15 junio). Play with Docker | Docker. Docker. https://www.docker.com/play-with-docker/
Docker Inc. (2023). Docker Documentation. Recuperado de https://docs.docker.com.
WordPress.org (2023). WordPress with Docker. Recuperado de https://wordpress.org.
¿Qué es Docker y cómo funciona? Ventajas de los contenedores Docker. (s. f.). https://www.redhat.com/es/topics/containers/what-is-docker






