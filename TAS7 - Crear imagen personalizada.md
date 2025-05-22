

## **1. Título**  
**Crear imagen personalizada**  

## **2. Tiempo de Duración**  
**30 minutos**  

---

## **3. Fundamentos**  
Despliegue de una aplicación React utilizando Docker, con los siguientes componentes:  
- **Frontend**: Aplicación React (Vite) contenerizada.  
- **Backend**: API simulada (mockAPI) para proveer datos.  
- **Comunicación**: Conexión entre frontend (puerto `5173`) y backend (puerto `3000`).  

**Características clave**:  
- Uso de `Dockerfile` para construir la imagen del frontend.  
- Persistencia de datos en el backend simulado.  
- Configuración declarativa para orquestación manual (sin `docker-compose.yml`).  

---

## **4. Conocimientos Previos**  
- Comandos básicos de Docker (`build`, `run`, `ps`).  
- Configuración de variables de entorno en React.  
- Manejo de repositorios Git.  

---

## **5. Objetivos Alcanzados**  
- Clonar y ejecutar el proyecto React localmente.  
- Crear un `Dockerfile` funcional para el frontend.  
- Generar una imagen Docker y desplegar el contenedor.  
- Configurar el backend simulado en un contenedor independiente.  
- Verificar la comunicación entre servicios.  

---

## **6. Equipo Utilizado**  
- **Computadora**: Asus Vivibook M1603QA (Ryzen 5, 16GB RAM, Fedora 41).  
- **Software**: Docker Engine, Node.js 18+, Git.  
- **Terminal**: Warp.  

---

## **7. Material de Apoyo**  
- Repositorio Frontend: [suda-frontend-s6](https://github.com/Daviddotcoms/suda-frontend-s6).  
- Repositorio Backend: [mockAPI](https://github.com/Daviddotcoms/mockAPI).  
- Documentación oficial:  
  - [Docker](https://docs.docker.com/).  
  - [Vite](https://vitejs.dev/).  

---

## **8. Procedimiento**  
Paso 1: Clonar el repositorio del frontend

```bash

# Instalar git  (aunque Fedora suele traerlo por defecto)
sudo dnf install git -y

# Clonar el repositorio
git clone https://github.com/Daviddotcoms/suda-frontend-s6.git

# Entrar al directorio del proyecto
cd suda-frontend-s6
```

Paso 2: Ejecutar el proyecto localmente
```
# Instalar Node.js y npm
sudo dnf install nodejs npm -y

# Verificar las versiones instaladas
node --version
npm --version
``` 

Instalar las dependencias del proyecto:

```bash

npm install
```

Mientras tanto, en otra terminal, vamos a configurar el backend simulado:

```

# Clonar el repositorio del mock API
git clone https://github.com/Daviddotcoms/mockAPI.git

# Entrar al directorio
cd mockAPI

# Instalar las dependencias
npm install

# Iniciar el servidor mock (se ejecutará en el puerto 3001)
npm start
```
 Regresar a la terminal del frontend y ejecuta:

```bash

# Iniciar la aplicación React (se ejecutará en el puerto 3000)
npm start
```
 Verificar que la aplicación funciona correctamente abriendo http://localhost:3000 en el navegador.

Paso 3: Crear el Dockerfile
Dentro del directorio suda-frontend-s6, crear un archivo llamado Dockerfile:

```bash

nano Dockerfile
```
 Copiar el siguiente contenido en el Dockerfile:

```bash

# Usa la imagen oficial de Node como base
FROM node:18-alpine as build

# Establece el directorio de trabajo
WORKDIR /app

# Copia los archivos de configuración del proyecto
COPY package*.json ./

# Instala las dependencias
RUN npm install

# Copia el resto de los archivos del proyecto
COPY . .

# Construye la aplicación para producción
RUN npm run build

# Usa Nginx para servir la aplicación
FROM nginx:alpine

# Copia los archivos construidos al directorio de Nginx
COPY --from=build /app/build /usr/share/nginx/html

# Expone el puerto 80
EXPOSE 80

# Comando para iniciar Nginx
CMD ["nginx", "-g", "daemon off;"]
```



Paso 4: Generar la imagen Docker

Construir la imagen Docker:

```bash
docker build -t suda-frontend .
```

 Verificar que la imagen se ha creado correctamente:

```bash

docker images
```

Se deberia  ver la imagen suda-frontend en la lista.
Paso 5: Crear el contenedor con la aplicación

Primero, se necesita asegurar de que el backend simulado esté disponible. Se puede  contenerizarlo también:

En el directorio mockAPI:
```bash

nano Dockerfile
```
Contenido para el Dockerfile del backend:
dockerfile
```bash
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3001

CMD ["npm", "start"]
```

Construir la imagen del backend:
```bash

docker build -t mock-api .
```

Ejecutar el contenedor del backend:
```bash
docker run -d -p 3001:3001 --name mock-api-container mock-api
```

 Ahora ejecutar el contenedor del frontend, conectándo al backend:

```bash

docker run -d -p 3000:80 --name suda-frontend-container suda-frontend
```
 Verificar que ambos contenedores están en ejecución:

```bash

docker ps
```
- - -

## **9. Resultados Esperados**  
1. **Frontend**: Interfaz React accesible en el puerto `5173`.

2. **Backend**: API simulada respondiendo en `3000`.
  
3. **Comunicación**: El frontend consume datos del backend sin errores. Y verificar que ambos contenedores esten en ejecución


```bash
# Verificar contenedores activos
docker ps
```
  ![Captura desde 2025-05-22 14-47-17](https://github.com/user-attachments/assets/d59c8bc5-0b7c-4abb-855f-0448b8009980)
   ![Captura desde 2025-05-22 14-55-50](https://github.com/user-attachments/assets/c3585c20-7a6c-4666-ab92-9000066578f7)
   ![Captura desde 2025-05-22 14-57-46](https://github.com/user-attachments/assets/45a1cce6-07f7-48e9-b5d9-e3a1be14d2df)
   ![Captura desde 2025-05-22 14-58-04](https://github.com/user-attachments/assets/4fd2668a-a30e-4f6d-9884-94f77fc46427)


  [Escuchar resumen](https://drive.google.com/file/d/1VkJfGiQjUsifoCmaCXDx_I9r3Vv4DXuV/view?usp=drive_link) 



## **11. Bibliografía**  
- Docker Documentation. (2023). *Best practices for writing Dockerfiles*.  
- Vite.js. (2023). *Guía de configuración para producción*.  

---
