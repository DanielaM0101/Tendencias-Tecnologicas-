


## 1. Título

**Wordpress con docker compose YML**

## 2. Tiempo de duración

**40 minutos**  

## 3. Fundamentos

Creación de un archivo docker-compose.yml para desplegar:

- WordPress: CMS basado en PHP/MySQL.

- MySQL: Base de datos para almacenar contenido.

- phpMyAdmin: Interfaz web de administración de MySQL.

Características clave:

- Uso de volúmenes para persistencia de datos.

- Red aislada para comunicación segura entre contenedores.

- Configuración declarativa en formato YAML.



## 4. Conocimientos previos

- Sintaxis YAML.

- Comandos básicos de Docker (docker compose up, down).

- Conceptos de redes y volúmenes en Docker.


## 5. Objetivos a alcanzar

- Crear un archivo docker-compose.yml funcional.

- Definir tres servicios interconectados.

- Configurar una red personalizada.

 - Implementar volúmenes persistentes.


## 6. Equipo necesario

- Computadora Asus vivibook M1603QA RYZEN 5 16GB 512G   fedora  Docker instalado.
- Conexión a internet.
- Navegador web compatible (Chrome, Firefox).
- Terminal: Warp



## 7. Material de apoyo

- Guía de la asignatura
- Documentación de Docker Compose

- WordPress en Docker Hub

- phpMyAdmin en Docker Hub
## 8. Procedimiento

### Paso 1: Crear el archivo docker-compose.yml
Crea un directorio para el proyecto:
```bash
mkdir wordpress-docker && cd wordpress-docker
```
Crea el archivo docker-compose.yml:
```bash
nano docker-compose.yml
```

Colocar el contenido:
```bash
services:
  wordpress:
    image: wordpress:latest
    container_name: wordpress
    restart: unless-stopped
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wppassword
      WORDPRESS_DB_NAME: wpdb
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8000:80"
    networks:
      - wp-network
    depends_on:
      - db

  db:
    image: mariadb:latest
    container_name: mariadb
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: wpdb
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wppassword
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - wp-network
    healthcheck:
      test: ["CMD-SHELL", "mysqladmin ping -u root -prootpassword"]
      interval: 5s
      timeout: 5s
      retries: 10

  phpmyadmin:
    image: phpmyadmin:latest
    container_name: phpmyadmin
    restart: unless-stopped
    environment:
      PMA_HOST: db
      PMA_USER: wpuser
      PMA_PASSWORD: wppassword
    ports:
      - "8080:80"
    networks:
      - wp-network
    depends_on:
      - db

volumes:
  wordpress_data:
  db_data:

networks:
  wp-network:
    driver: bridge
```
### Paso 2: Ejecutar Docker Compose
Levanta los contenedores:
```bash
sudo docker-compose up -d
```
Verifica que los contenedores estén corriendo:
```bash
sudo docker ps
```
### Paso 3: Acceder a WordPress y phpMyAdmin
En el navegador web.

WordPress:

Entra a:
http://localhost:8000


phpMyAdmin:

Entra a:
 http://localhost:8080


## Resultados Esperados

Al acceder a los puertos expuestos, se obtuvieron los siguientes resultados:

![image](https://github.com/user-attachments/assets/5a9c0f21-3f69-4c11-a6fc-2c88c4f0a5d2)

Figura 1-1. WordPress en ejecución


![image](https://github.com/user-attachments/assets/1eef2606-5a3c-46e3-89b5-17b03423f515)

Figura 1-2. phpMyAdmin con la base de datos

![image](https://github.com/user-attachments/assets/3e064d2c-b8c6-43aa-8605-45d5b188a11a)
Figura 1-3 Verificar los contenedores


[Escuchar resumen](https://drive.google.com/file/d/1RTJGpQaM_wE_-oueKarHgqoC6LE57qAF/view?usp=sharing)
Resumen en formato audio
 
 
## Bibliografia 
Docker Inc. (2023). Docker Compose documentation. https://docs.docker.com/compose/

MySQL. (2023). Official MySQL Docker image. https://hub.docker.com/_/mysql
