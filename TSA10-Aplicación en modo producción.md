

## 1. Título  
**Implementación y Configuración de un Servidor Web Nginx en Contenedores Docker**

## 2. Tiempo de duración  
**3 horas**

## 3. Fundamentos
Un servidor web es un software que procesa solicitudes a través del protocolo HTTP, entregando contenido a los clientes que lo solicitan, típicamente navegadores web. Entre los servidores web más populares se encuentra Nginx, un servidor de alto rendimiento conocido por su eficiencia, estabilidad y bajo consumo de recursos.

Nginx (pronunciado "engine-x") fue creado originalmente por Igor Sysoev en 2004 para resolver el problema C10K (manejar 10,000 conexiones concurrentes). A diferencia de servidores web tradicionales que crean un nuevo proceso o hilo para cada conexión, Nginx utiliza una arquitectura asíncrona y orientada a eventos, lo que le permite manejar múltiples conexiones dentro de un solo proceso de trabajo.

La containerización, por otro lado, es una tecnología que permite empaquetar una aplicación junto con todas sus dependencias en una unidad estandarizada llamada contenedor. Docker es la plataforma de containerización más popular, que permite crear, distribuir y ejecutar aplicaciones en contenedores. Los contenedores son ligeros, portátiles y aislados, lo que facilita la implementación de aplicaciones en diferentes entornos.

La combinación de Nginx y Docker proporciona una solución potente para implementar servidores web. Al ejecutar Nginx en un contenedor Docker, obtenemos beneficios como:

1. **Portabilidad**: El servidor web puede ejecutarse de manera consistente en cualquier entorno que tenga Docker instalado.
2. **Aislamiento**: El servidor web se ejecuta en un entorno aislado, lo que mejora la seguridad y evita conflictos con otras aplicaciones.
3. **Escalabilidad**: Es fácil crear múltiples instancias del servidor web para manejar aumentos en el tráfico.
4. **Facilidad de configuración**: La configuración del servidor web se puede versionar y compartir fácilmente.

Nginx puede funcionar como servidor web, proxy inverso, balanceador de carga y caché HTTP. En esta práctica, nos enfocaremos en su función como servidor web para servir contenido estático. La configuración básica de Nginx se realiza a través de archivos de configuración con una sintaxis específica, donde se definen los servidores virtuales, las ubicaciones, las reglas de enrutamiento y otras directivas.

Para implementar Nginx en Docker, se uso una imagen oficial de Nginx disponible en Docker Hub. Esta imagen incluye Nginx preinstalado y configurado con valores predeterminados, pero podemos personalizarla según nuestras necesidades proporcionando nuestros propios archivos de configuración y contenido web.

## 4. Conocimientos previos  
Para realizar esta practica se necesita tener claro los siguientes temas:
- Comandos básicos de Linux (cd, ls, mkdir, etc.)
- Conceptos básicos de redes (HTTP, puertos, direcciones IP)
- Fundamentos de servidores web
- Conocimientos básicos de Docker (imágenes, contenedores, volúmenes)
- Editor de texto en terminal (vim, nano)

## 5. Objetivos a alcanzar  
- Implementar un servidor web Nginx utilizando contenedores Docker
- Configurar correctamente Nginx para servir contenido estático
- Personalizar la configuración de Nginx mediante archivos de configuración
- Utilizar volúmenes de Docker para persistir datos y configuraciones
- Comprender la estructura de los archivos de configuración de Nginx
- Implementar múltiples sitios web (hosts virtuales) en un solo servidor Nginx
- Configurar reglas de redirección y reescritura en Nginx

## 6. Equipo necesario  

- Computador con sistema Linux 41
- Docker Desktop v4.x o superior instalado y funcionando
- Conexión a Internet para descargar imágenes de Docker
- Navegador web moderno 
- Mínimo 4GB de RAM y 10GB de espacio libre en disco
- Terminal o línea de comandos

## 7. Material de apoyo  

   
- Documentación oficial de Docker: https://docs.docker.com/
- Documentación oficial de Nginx: https://nginx.org/en/docs/
- Imagen oficial de Nginx en Docker Hub: https://hub.docker.com/_/nginx
- Guía de comandos básicos de Linux: https://www.linuxfoundation.org/blog/blog/classic-sysadmin-linux-command-line-cheat-sheet
- Repositorio de ejemplos de configuración de Nginx: https://github.com/nginx/nginx-wiki 
- Guía de la asignatura y material proporcionado por el profesor.  
- Repositorios y documentacion en clase

## 8. Procedimiento  

**Paso 1:**  Crear estructura del proyecto
```bash
PROYECT_SUPERMERCADO/
├── frontend/   # React
├── backend/    # Flask
└── docker-compose.yml

```


**Paso 2:**   Configuración de Flask
Se definió un endpoint /api/data y conexión a PostgreSQL:

![Captura desde 2025-06-14 19-10-14](https://github.com/user-attachments/assets/e07aca18-7b6e-4a24-970f-a3a68abc66eb)


**Paso 3:**  Docker Compose
Archivo YAML con servicios para:
  Frontend (React + Nginx).
  Backend (Flask).
  PostgreSQL + PgAdmin.
  ![imagen](https://github.com/user-attachments/assets/245822b7-1afb-4843-9bd5-37a8d3928394)



**Paso 4:** Ejecutar el proyecto
```bash
docker-compose up --build
```
![imagen](https://github.com/user-attachments/assets/c26c5cdd-4f87-41ae-af4a-e3a691ca9676)


**Paso 6:** Verificar resultados
  Frontend: Accesible en http://localhost.
  ![imagen](https://github.com/user-attachments/assets/53961c04-0e2b-4da0-8610-b9e9d2bb8074)


  Backend: Responde en http://localhost/api/data.
![imagen](https://github.com/user-attachments/assets/57f1b7b0-72a2-4fb6-9a41-e2130e237e0c)

  PgAdmin: Interfaz en http://localhost:5050.
 ![imagen](https://github.com/user-attachments/assets/5c006056-3daf-45ae-abfe-b4551ef8f003)

## 9. Resultados esperados

Al finalizar esta práctica, se deberia haber logrado:

1. Implementar un servidor web Nginx en un contenedor Docker.
2. Personalizar la configuración de Nginx para servir contenido estático.
3. Utilizar volúmenes de Docker para persistir datos y realizar cambios en tiempo real.
4. Configurar múltiples sitios web (hosts virtuales) en un solo servidor Nginx.

## Resumen en formato audio
[Escuchar resumen](https://drive.google.com/file/d/1cdiWFBgGhThUDgJlkwZA6KH0hqd7qpH8/view?usp=drive_link)



## 10. Bibliografía
- React Team. (2024). React Documentation. https://react.dev/
- Node.js Foundation. (2024). Node.js Documentation. https://nodejs.org/
- PostgreSQL Global Development Group. (2024). PostgreSQL Documentation. https://www.postgresql.org/
- Docker Inc. (2024). Docker Documentation. https://docs.docker.com/
- Nginx. (2024). Nginx Documentation. https://nginx.org/en/docs/

