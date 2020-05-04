# Paso Instalación

Composer es una herramienta para gestionar las dependencias en PHP. Te permite declarar las librerías de las cuales tu proyecto depende o necesita y las instala en el proyecto por ti, si deseas saber más acerca de Composer lee el siguiente [post](https://styde.net/que-es-composer-y-como-usarlo).

Para instalar Composer en Windows debemos descargarlo de su [página oficial ](https://getcomposer.org/download)y en la sección Windows Installer, haz click en Composer-Setup.exe.

![](../../.gitbook/assets/image%20%2813%29.png)

Una vez que la descarga finalice, ejecuta el instalador y haz click en Next.

![Composer Setup](https://styde.net/wp-content/uploads/2014/11/02.png)

Si quieres administrar tus proyectos mediante el Explorador de Windows puedes seleccionar la opción «Install Shell Menus» aunque lo recomendable es la usar la línea de comandos.

![Composer](https://styde.net/wp-content/uploads/2014/11/03.png)

A continuación nos pide que indiquemos la ruta del ejecutable de PHP, en mi caso como estoy trabajando con XAMPP el ejecutable de PHP se encuentra en la ruta C:\xampp\php\ \(si usas WAMPP la ruta es C:\wamp\bin\php\php5.5.12\) y seleccionas php.exe, luego click en Next.

![Composer PHP](https://styde.net/wp-content/uploads/2014/11/04.png)

En este punto el instalador de Composer nos muestra la configuración de la instalación, simplemente le damos click a Install.

![Composer Windows](https://styde.net/wp-content/uploads/2014/11/05.png)

Una vez esté todo instalado, aparecerán otras donde simplemente debes hacer click en Next, y posteriormente en Finalizar; después de tantos Next, Next típicos de Windows el instalador de Composer habrá puesto en nuestro PATH global la ruta de la carpeta PHP y su propia carpeta Composer. Esto nos permite trabajar desde consola escribiendo sólo php o composer sin necesidad de indicar la ruta del ejecutable. Para ver que todo está en orden vamos a realizar dos pequeñas pruebas, así que es momento de abrir la consola, y teclear:

`composer -version (tecla Enter)`

Esto debería devolver la versión de cada uno, como se ve en la siguiente imagen:

![Comandos Composer](https://styde.net/wp-content/uploads/2014/11/06.png)

Con esto ya tenemos Composer instalado y funcionando en Windows, ahora solo nos queda instalar Laravel, veamos cómo hacer esto posible.

### 

