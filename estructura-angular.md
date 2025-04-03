## 1. Título  
Creación de la Estructura de un Proyecto Angular en Linux mediante Comandos  

## 2. Tiempo de duración  
Aproximadamente 30 minutos  

## 3. Fundamentos  
Angular es un framework de desarrollo web  que esta basado en TypeScript que permite crear aplicaciones web escalables y modulares. La creación de un proyecto Angular normalmente se realiza con Angular CLI, pero también es posible estructurarlo manualmente mediante comandos de Linux, lo que proporciona un mejor entendimiento del funcionamiento de sus directorios y archivos esenciales.  

Linux es un sistema operativo ampliamente utilizado en el desarrollo de software debido a su estabilidad y flexibilidad. Su terminal permite la manipulación de archivos y directorios mediante comandos, lo cual es esencial para la organización de proyectos.  

A continuación, se detallan los principales comandos utilizados:  
- `mkdir`: Crea directorios.  
- `touch`: Crea archivos vacíos.  
- `ls`: Lista archivos y directorios.  
- `tree`: Muestra la estructura de directorios en forma de árbol.  

*Figura 1-1. Estructura del proyecto generada manualmente con comandos Linux 
![image](https://github.com/user-attachments/assets/05118e05-938e-450c-ab04-b20ad644a764)


## 4. Conocimientos previos  
Para realizar esta práctica, es necesario tener claros los siguientes temas:  
- Comandos básicos de Linux (mkdir, touch, ls, tree)  
- Manejo básico de terminal  
- Conceptos de Angular y su estructura de archivos  

## 5. Objetivos a alcanzar  
- Implementar la estructura de un proyecto Angular manualmente mediante comandos de Linux.  
- Comprender la función de cada directorio y archivo dentro del proyecto.  
- Verificar la estructura generada utilizando herramientas de terminal.  

## 6. Equipo necesario  
- Computador con sistema operativo Linux (Fedora)
-  Asus vivibook
  M1603QA
  RYZEN 5
  16GB
  512G
 - Terminal de comandos  (WARP)

## 7. Material de apoyo  
- Documentación oficial de Angular  
- Guía de uso de terminal Linux  
- Referencias sobre comandos básicos de Linux  

## 8. Procedimiento  

### Paso 1: Abrir la terminal  
Para comenzar, abrir la terminal en el sistema Linux. En la mayoría de distribuciones, se puede hacer con la combinación de teclas `Ctrl + Alt + T`.  

### Paso 2: Moverse a la ubicación donde se  creara el proyecto  
Se crea el proyecto en la carpeta "Documentos", dentro de otra llamada tendenciasTecnologicas para esto se  escribe:  
```bash  
cd ~/Documentos
mkdir tendenciasTecnologicas
```
### Paso 3: Comando  mkdir -p
mkdir: Este comando se usa para crear directorios (carpetas).

-p: La opción -p le dice a mkdir que cree toda la estructura de carpetas de forma recursiva. Si alguna carpeta intermedia no existe, mkdir la creará automáticamente.
```bash  
mkdir -p estructura-angular/src/app/components estructura-angular/src/assets/images estructura-angular/src/assets/fonts estructura-angular/src/assets/styles estructura-angular/dist estructura-angular/public

```
### Paso 4: Comando touch
touch: Este comando se usa para crear archivos vacíos. Si el archivo ya existe, actualiza su fecha de acceso y modificación.

Este comando crea todos los archivos necesarios para la estructura del proyecto. Todos los archivos estarán vacíos, solo tienen el nombre.
```bash  
touch estructura-angular/src/app/app.component.ts estructura-angular/src/app/app.component.html estructura-angular/src/app/app.component.css estructura-angular/src/app/app.module.ts estructura-angular/src/index.html estructura-angular/src/main.ts estructura-angular/src/styles.css estructura-angular/src/favicon.ico estructura-angular/angular.json estructura-angular/package.json estructura-angular/tsconfig.json estructura-angular/README.md

```

### Paso 5:  Instalar tree 
En algunas distribuciones no viene instalado por defecto. Para instalarlo, en fedora se usa:
```bash
sudo dnf install tree
```

### Paso 6: Ver la estructura en forma de árbol
Entrar a la carpeta del proyecto:
```bash
cd estructura-angular
```

Luego, ejecutar:
```bash
tree
```
## Resultados esperados
Al desarrollar esta  práctica, se obtuvo  una estructura de proyecto Angular correctamente organizada y visualible en la terminal mediante el comando tree. Además, se logró  desarrollar habilidades en la manipulación de archivos y directorios en Linux.

![image](https://github.com/user-attachments/assets/98da3efb-9a7b-4713-a093-f359f7c28875)


*Figura 1-2.Comandos linux utilizados y resultado final.
## Blibiografia
Optimiza tu Proyecto Angular: Guía Completa de Estructura de Carpetas. (2024, 15 julio). https://amoelcodigo.com/posts/angular-folders/
A, D., & A, D. (2025, 17 marzo). Los 40 comandos de Linux más populares y utilizados en para 2025. ES Tutoriales. https://www.hostinger.es/tutoriales/linux-comandos
