# Crear  el proyecto

### Creando proyecto en Laravel

Existen dos formas de crear un proyecto con Laravel, la primera es descargando el archivo master desde su [repositorio oficial de GitHub](https://github.com/laravel/laravel/archive/master.zip) y la otra es usando Composer desde la consola que es precisamente lo que haremos en esta ocasión.

Desde la consola, dirígete al directorio donde guardas tus proyectos web \(si usas XAMPP la ruta es C:\xampp\htdocs para WAMPP es C:\wamp\www\), y teclea lo siguiente:

`cd C:\xampp\htdocs`  

Ahora crearemos el proyecto laravel escribiendo las siguientes palabras mágicas:

`composer create-project laravel/laravel nombre_del_proyecto --prefer-dist`

En mi caso en un arranque de creatividad llamaré a mi proyecto “pruebita”

![Laravel Composer](https://styde.net/wp-content/uploads/2014/11/laravel-composer.png)

Composer empezará a descargar las librerías necesarias para nuestro proyecto, esto requiere un poco de tiempo.

![Composer descarga](https://styde.net/wp-content/uploads/2014/11/composer-descarga-paquetes.png)

Si no ocurrió algún problema de conexión a Internet veremos que nuestro proyecto “pruebita” se creó correctamente.

[  
](https://styde.net/wp-content/uploads/2014/11/composer-descarga-paquetes.png)

![Laravel Composer](https://styde.net/wp-content/uploads/2014/11/proyecto-creado-composer-laravel.png)

Finalmente para verificar que la creación de nuestro proyecto “pruebita” se realizó de manera correcta, accede a http://localhost/nombre\_del\_proyecto/public en el navegador de tu preferencia, donde debes ver lo siguiente:

![Laravel Chrome](https://styde.net/wp-content/uploads/2014/11/proyecto-laravel-navegador-windows-1024x727.png)

¡Felicidades! Ahora puedes dar rienda suelta a tu imaginación y crear aplicaciones geniales con Laravel.

