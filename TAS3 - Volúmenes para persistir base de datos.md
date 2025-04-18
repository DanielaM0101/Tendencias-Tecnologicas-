
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
- Cliente de PostgreSQL (psql) o herramienta gráfica (TablePlus, DataGrip).

## 7. Material de apoyo.
   
- Documentación oficial de Docker
- Guía rápida de comandos PostgreSQL
- Tutorial de volúmenes en Docker
-  Guía de la asignatura
  
## 8. Procedimiento

(Enumerar el paso a paso, las imágenes deben tener títulos.)
Paso 1: xxxxx
Paso 2: xxxxx

Figura 1-1. Diagrama de contenedores.
Las figuras un ancho máximo de 800px

## 9. Resultados esperados:
    
Descripcion de los resultados, capturas de pantallas del resultado final de la practica

## 10. Bibliografía
    
- Apellido,..... En apa
