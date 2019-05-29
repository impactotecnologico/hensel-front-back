# Introducción

En el presente README se documenta lo necesario para el desarrollo de la api backend del asistente de migración de propiedades desde Fotocasa al sitio web de Estudio Hensel de la Vega

### Dependencias

Para que el proyecto funcione se debe tener en nuestro entorno:

+ **php 7 o superior**
+ **php curl**
+ **Slim 3.0**
+ **composer**

### Instalación inicial

Una vez clonado el repositorio, ir al directorio de backend y ejecutar desde una terminal **php composer.phar install** (o **composer install** dependiendo de la versión de composer local)

Con esto tendremos el core de la app con Slim en nuestro sistema local

Además, debemos asegurarnos de tener un .htaccess en la raíz del directorio backend con el contenido mostrado a continuación:

	RewriteEngine on
	RewriteCond %{REQUEST_FILENAME} !-d
	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteRule . index.php [L]

### Despliegue

La api está desplegada en un subdominio de la web de Estudio Hensel de la Vega, en concreto, podemos acceder a través de la url: **http://api.estudiohenseldelavega.es/**

Para desplegar nuevas versiones, basta con acceder al **cpanel**, ir al directorio **public_html** en el administrador de archivos y reemplazar el contenido o archivos editados del directorio **api**

**Nota:** para asegurar el funcionamiento, mantener la permisología actual de los archivos del directorio de la api

#### Campos de bd y data retornada a almacenar

Listado por tablas de Wordpress, se está tomando como guía la data del post con id **1487**:
**wp_post**

* **id:** automático
* **post_author:** 1
* **post_date:** realEstates.date
* **post_date_gmt:** realEstates.date
* **post_modified:** realEstates.date
* **post_content:** realEstates.description
* **post_title:** realEstates.description
* **post_status:** publish
* **comment_status:** closed
* **ping_status:** closed
* **post_name:** realEstates.description (reemplazando blanks con "-")
* **post_parent:** 0
* **post_type:** property
* **post_mime_type:** ''
* **id_fotocasa:** realEstates.id
* **post_excerpt:** ''
* **to_ping:** ''
* **pinged:** ''
* **post_content_filtered:** ''

**imágenes**

* **id:** automático
* **post_author:** 1
* **post_date:** realEstates.date
* **post_date_gtm:** realEstates.date
* **post_content:** null
* **post_title:** realEstates.description
* **post_status:** inherit
* **comment_status:** open
* **ping_status:** closed
* **post_name:** realEstates.description (reemplazando blanks con "-")
* **post_parent:** 0
* **post_type:** attachment
* **post_mime_type:** image/png
* **guid:** realEstates.multimedias[x].url
* **post_excerpt:** ''
* **to_ping:** ''
* **pinged:** ''
* **post_content_filtered:** ''


**wp_postmeta**

**wp_postmeta (precio)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_property_price
* **meta_value:** realEstates.transactions[0].value[0]

**wp_postmeta (dimensiones)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_property_size
* **meta_value:** realEstates.features[0].value[x] (donde el key sea "surface")

**wp_postmeta (unidad de medida)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_property_size_postfix
* **meta_value:** m2

**wp_postmeta (habitaciones)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_property_bedrooms
* **meta_value:** realEstates.features[0].value[x] (donde el key sea "rooms")

**wp_postmeta (baños)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_property_bathrooms
* **meta_value:** realEstates.features[0].value[x] (donde el key sea "bathrooms")

**wp_postmeta (mapa)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_property_map
* **meta_value:** 0

**wp_postmeta (dirección)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_property_address
* **meta_value:** realEstates.address.ubication + " " + realEstates.address.location.country + realEstates.address.location.upperlevel

**wp_postmeta (coordenadas)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_property_location
* **meta_value:** realEstates.address.coordinates.latitude + "," + realEstates.address.coordinates.longitude

**wp_postmeta (imágenes)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_property_images
* **meta_value:** id del post de tipo attachment 

**wp_postmeta (agente)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_agent_display_option
* **meta_value:** none

**wp_postmeta (agente)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_agents
* **meta_value:** -1

**wp_postmeta (featured)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_featured
* **meta_value:** 0

**wp_postmeta (slider)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** REAL_HOMES_add_in_slider
* **meta_value:** no

**wp_postmeta (seo1)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** _yoast_wpseo_primary_property-type
* **meta_value:** 57

**wp_postmeta (seo2)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** _yoast_wpseo_primary_property-city
* **meta_value:** 54

**wp_postmeta (seo3)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** _yoast_wpseo_primary_property-status
* **meta_value:** 55

**wp_postmeta (seo4)**
* **meta_id:** automático
* **post_id:** id del post creado
* **meta_key:** _yoast_wpseo_metadesc
* **meta_value:** ✅ Estudio Colombia ✅ empresa líder en venta y alquiler de INMUEBLES en San Lorenzo-Hortaleza con transparencia y confianza.