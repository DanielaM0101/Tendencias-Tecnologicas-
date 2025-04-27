# Práctica: Implementación de MySQL y phpMyAdmin en contenedores Docker

## 1. Título  
**Despliegue de un entorno de gestión de bases de datos con MySQL y phpMyAdmin utilizando Docker**

## 2. Tiempo de duración  
⏱️ 45 minutos 

## 3. Fundamentos  
Los contenedores Docker proporcionan un entorno aislado para ejecutar aplicaciones con todas sus dependencias. En esta práctica utilizamos dos tecnologías clave: **MySQL** (sistema de gestión de bases de datos relacionales que utiliza SQL) y **phpMyAdmin** (aplicación web para administrar MySQL mediante interfaz gráfica). Las redes en Docker permiten la comunicación entre contenedores aislados mediante una red bridge personalizada.

![image](https://github.com/user-attachments/assets/73e1ce7c-bd11-45d3-b34b-91bec9e58f19)
 
*Figura 1. Arquitectura de contenedores Docker*

## 4. Conocimientos previos  
- Comandos básicos de Linux - Conceptos básicos de Docker (imágenes, contenedores, redes) - Manejo de navegador web - Conceptos fundamentales de bases de datos - Uso de terminal/consola de comandos

## 5. Objetivos  
- Implementar contenedores Docker para MySQL y phpMyAdmin - Crear y configurar una red personalizada en Docker - Establecer comunicación entre contenedores - Gestionar bases de datos mediante interfaz gráfica - Crear una base de datos de prueba desde phpMyAdmin

## 6. Equipo necesario  
- Computador con sistema operativoLinux  fedora
- -Computadora Asus vivibook M1603QA RYZEN 5 16GB 512G
- Computador con Docker instalado (linux fedora)
- Consola Warp

## 7. Material de apoyo  
- [Documentación oficial de Docker](https://docs.docker.com/) - [Documentación de MySQL](https://dev.mysql.com/doc/) - [phpMyAdmin documentation](https://www.phpmyadmin.net/docs/) - Cheat sheet de comandos Docker
- Video de clase 

## 8. Procedimiento  
1. Crear red Docker: `docker network create mysql-network`  
2. Implementar contenedor MySQL: `docker run -d --name mysql-container --network mysql-network -e MYSQL_ROOT_PASSWORD=rootpassword -p 3306:3306 mysql:8.0`  
3. Implementar contenedor phpMyAdmin: `docker run -d --name phpmyadmin-container --network mysql-network -e PMA_HOST=mysql-container -p 8080:80 phpmyadmin/phpmyadmin`  
4. Verificar contenedores en ejecución: `docker ps`  
![Captura desde 2025-04-26 20-08-34](https://github.com/user-attachments/assets/44bc4270-81c7-4fdb-95b6-ba8bb2ec5bf3)

*Figura 2. Interfaz de phpMyAdmin*

## 9. Resultados esperados  
Al acceder a http://localhost:8080 deberíamos ver la interfaz de phpMyAdmin donde podremos: 1. Iniciar sesión con las credenciales configuradas (root/rootpassword) 2. Navegar por la interfaz gráfica 3. Crear una nueva base de datos de prueba
![image](https://github.com/user-attachments/assets/4d568c69-7131-48ab-8cb7-503b306c3a83)
*Figura 3. Interfaz de phpMyAdmin  en la base de datos*
![image](https://github.com/user-attachments/assets/353ee9d9-90f8-44bd-9c76-a8143112079b)
*Figura 4. Comandos utilizados 

## 10. Bibliografía  
- Docker, Inc. (2023). Docker documentation. https://docs.docker.com/  
- MySQL AB. (2023). MySQL 8.0 Reference Manual. https://dev.mysql.com/doc/  
- The phpMyAdmin Project. (2023). phpMyAdmin user documentation. https://www.phpmyadmin.net/docs/
