# Introducción

En este README se documenta lo necesario para el desarrollo y despliegue del frontend del panel administrativo para importación y migración de propiedades a la web de **Estudio Hensel de la Vega** desde la red de **Fotocasa.**

## Tecnologías

+ Bootstrap 4.3.1 (cargado vía CDN en el index)
+ JQuery 3.3.1 (cargado vía CDN en el index)
+ Popper 1.14.7 (cargado vía CDN en el index como dependencia del core de Bootstrap) 

### Estructura de archivos

La web administrativa de migración de propiedades consta de los siguientes archivos:

+ **index.html**: único archivo de vistas donde se renderiza la opción de migración
+ **Carpeta assets:** directorio que contiene los estilos css, imágenes y scripts JS
+ **assets/js/script.js:** script que realiza las llamadas ajax a los endpoints de la api (no usa nada adicional, son llamadas ajax puras en JS)

### Despliegue

Para desplegar el admin, basta con ingresar a **https://estudiohenseldelavega.es/cpanel** e ingresar con las credenciales del cpanel, una vez ahí, ingresar en el administrador de archivos al directorio **public_html**, el asistente de migración está desplegado en el directorio **admin**

Para desplegar nuevas versiones basta con reemplazar los archivos del directorio **admin**