


## 1. Título  
**Despliegue de Aplicación Web para Gestión de Productos de Supermercado usando Docker, React y Flask*

## 2. Tiempo de duración  
**120 minutos (2 horas) para desarrollo completo y pruebas**  

## 3. Fundamentos
Esta práctica se centra en la contenerización de aplicaciones web modernas utilizando Docker, que es una plataforma de virtualización ligera que permite empaquetar software en unidades estandarizadas llamadas contenedores. A diferencia de las máquinas virtuales tradicionales, los contenedores comparten el kernel del sistema operativo host, lo que los hace más eficientes en uso de recursos.



![imagen](https://github.com/user-attachments/assets/0d91b6eb-2f31-480d-8cea-e7b32a53a1a0)


*Figura 1-1. Comparación entre virtualización tradicional (izquierda) y contenedores Docker (derecha).*

El proyecto implementa una arquitectura de dos capas:

   - Frontend: Desarrollado con React, una biblioteca JavaScript para construir interfaces de usuario. React utiliza un DOM virtual para actualizaciones eficientes y sigue el patrón de diseño de componentes.

  - Backend: Implementado con Flask, un microframework web Python que proporciona endpoints RESTful. La comunicación entre frontend y backend sigue el protocolo HTTP con datos en formato JSON.

Docker Compose permite orquestrar múltiples contenedores como un solo servicio. En este caso, coordina:

  - Un contenedor con servidor Nginx para el frontend

  - Un contenedor con Flask para el backend

  - Una red virtual que permite la comunicación entre ellos 
    

## 4. Conocimientos previos  
Para realizar esta práctica el estudiante necesita tener claro los siguientes temas:

  - Conceptos básicos de Docker y contenedores

  - Sintaxis básica de YAML para archivos docker-compose

  - Fundamentos de desarrollo web (HTML, CSS, JavaScript)

  - Conceptos básicos de React (componentes, estado, props)

  - Conocimiento elemental de APIs REST

  - Manejo de terminal Linux y comandos básicos

  - Comprensión de redes informáticas básicas (puertos, direcciones IP)

## 5. Objetivos a alcanzar  
  - Implementar una aplicación frontend en React contenerizada con Nginx

  - Configurar un backend API REST con Flask en un contenedor independiente

  - Establecer comunicación entre contenedores usando Docker Compose

  -  Manipular archivos de configuración para Nginx (reverse proxy)

   - Visualizar datos dinámicos en una interfaz tabular

   - Calcular y mostrar totales basados en datos del backend



## 6. Equipo necesario  
- Computadora Asus Vivibook M1603QA (Ryzen 5, 16GB RAM)
- Docker Engine 24.0.7
- Docker Compose v2.23.0
- Sistema operativo Linux (Fedora 41)  

## 7. Material de apoyo  
- Guía de la asignatura y material proporcionado por el profesor.  
- Documentación oficial de Docker: https://docs.docker.com/  
- Documentación de Flask: https://flask.palletsprojects.com/
- Guía de React: https://reactjs.org/docs/getting-started.html


## 8. Procedimiento  

**Paso 1:** Crear la carpeta principal:
```bash
mkdir supermercado-app
cd supermercado-app
  ```
Crear las subcarpetas:
```bash
mkdir backend frontend
  ```

**Paso 2:**  Configurar el Backend (API Flask).
Crear los archivos backend/app.py, backend/requirements.txt y backend/Dockerfile 
![imagen](https://github.com/user-attachments/assets/14efaf04-9d10-4309-a5a6-7e736006ced1)
![imagen](https://github.com/user-attachments/assets/d925aaf9-a2c1-43b8-ab1e-972c74e6f7a2)
![imagen](https://github.com/user-attachments/assets/8a157ef5-4993-4764-85bd-6a541ff67da5)
![imagen](https://github.com/user-attachments/assets/1b75e195-1984-49c5-bd20-fee72d9603d5)



**Paso 3:** Desarrollar el frontend React.
Crear componentes principales (ProductosTable.js, App.js) y archivos de configuración (Dockerfile, nginx.conf)
```bash
import React, { useState, useEffect } from 'react';

function ProductosTable() {
  const [productos, setProductos] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        console.log('Iniciando solicitud a la API...');
        // Siempre usar localhost en el navegador ya que es donde se ejecuta el código del cliente
        const apiUrl = 'http://localhost:5000/api/productos';

        const response = await fetch(apiUrl, {
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          }
        });

        console.log('Estado de la respuesta:', response.status);
        
        if (!response.ok) {
          throw new Error(`Error HTTP! estado: ${response.status}`);
        }

        const data = await response.json();
        console.log('Datos recibidos:', data);
        
        if (!data.productos) {
          throw new Error('Formato de datos incorrecto');
        }

        // Procesar los datos para asegurar que tengan la estructura correcta
        const productosProcessed = data.productos.map(producto => ({
          ...producto,
          // Inicializar cantidad y subtotal si no existen
          cantidad: producto.cantidad || 1,
          subtotal: producto.subtotal || producto.precio * (producto.cantidad || 1)
        }));
        
        setProductos(productosProcessed);
      } catch (err) {
        console.error('Error al obtener productos:', err);
        // Mensaje de error más detallado para ayudar al diagnóstico
        setError(`Failed to fetch: ${err.message}. Verifique que el backend esté accesible en http://localhost:5000`);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, []);

  if (loading) return <div>Cargando productos...</div>;
  if (error) return <div>Error al cargar productos: {error}</div>;

  // Calcular el total asegurándose de que subtotal existe
  const total = productos.reduce((sum, producto) => {
    const subtotal = producto.subtotal || producto.precio * (producto.cantidad || 1);
    return sum + subtotal;
  }, 0);

 return (
    <div className="productos-container">
      <h2>Productos Escaneados</h2>
      <table className="productos-table">
        <thead>
          <tr>
            <th>ID</th>
            <th>Nombre</th>
            <th>Precio Unitario</th>
            <th>Cantidad</th>
            <th>Subtotal</th>
          </tr>
        </thead>
        <tbody>
          {productos.map(producto => (
            <tr key={producto.id}>
              <td>{producto.id}</td>
              <td>{producto.nombre}</td>
              <td>${producto.precio.toFixed(2)}</td>
              <td>{producto.cantidad}</td>
              <td>${producto.subtotal.toFixed(2)}</td>
            </tr>
          ))}
        </tbody>
        <tfoot>
          <tr>
            <td colSpan="4" style={{textAlign: 'right'}}><strong>Total:</strong></td>
            <td><strong>${total.toFixed(2)}</strong></td>
          </tr>
        </tfoot>
      </table>
    </div>
  );
}

export default ProductosTable;
  ```

![imagen](https://github.com/user-attachments/assets/d347a1c5-2cb1-4128-9248-2a1846769d31)
![imagen](https://github.com/user-attachments/assets/f5605b87-7324-44c5-80e0-c5bc13b09c5b)


**Paso 4:** Configurar docker-compose.yml
Definir los servicios para backend y frontend con sus respectivas configuraciones de red
![imagen](https://github.com/user-attachments/assets/1cdbc698-5e74-4f77-9e09-fddbce50376c)



**Paso 5:**  Construir las imágenes
```bash
docker-compose build
  ```

![imagen](https://github.com/user-attachments/assets/b345f2ee-fcef-4bb8-8843-135267cadf28)

Iniciar los contenedores
```bash
docker-compose up
  ```

![imagen](https://github.com/user-attachments/assets/8df6242a-3832-473b-89ba-04981c6a5092)
![imagen](https://github.com/user-attachments/assets/20607aa2-f78f-4738-8de3-4dde656d636b)



**Paso 7:** Verificar funcionamiento.
    Abrir el navegador en http://localhost:3000
    Debería verse la tabla de productos con el total

![imagen](https://github.com/user-attachments/assets/7bf6d2ad-70bc-45ff-9f29-fc877663279b)

    
   Visitar http://localhost:5000/api/productos
   Debería verse los datos en formato JSON
    
  ![imagen](https://github.com/user-attachments/assets/40f04cbe-59ea-46e1-bf19-8e60c64fca21)



## 9. Resultados esperados  
Al completar la práctica, deberían ser visibles los siguientes resultados:
- Una interfaz web con el título "Supermercado App"
- Una tabla que muestra los productos de ejemplo (Leche, Pan, Galletas)
- Columnas con: ID, Nombre, Precio Unitario, Cantidad y Subtotal
- Un pie de tabla con el total calculado de la compra
- ULa aplicación debe responder sin errores en la consola del navegador.

## Resumen en formato audio
[Escuchar resumen](https://drive.google.com/file/d/1cdiWFBgGhThUDgJlkwZA6KH0hqd7qpH8/view?usp=drive_link)


 

## 10. Bibliografía
Docker, Inc. (2022). Docker documentation. https://docs.docker.com/

Fielding, R. (2000). Architectural Styles and the Design of Network-based Software Architectures. University of California, Irvine.

Flask Project. (2022). Flask documentation. https://flask.palletsprojects.com/

React Community. (2022). React documentation. https://reactjs.org/docs/getting-started.html

Microsoft. (2022). Docker containers overview. https://docs.microsoft.com/en-us/virtualization/windowscontainers/about/

