# Los Seeder

Los seeders, son un recurso que nos permite cargar información a nuestras tablas para probar de manera sencilla y rápida el funcionamiento de nuestra aplicación \(paginación, filtros, entre otros\). Ya basta de estar insertando datos uno por uno, inventando nombres o colocando el típico y horrible “asdffasd” o “123”.

Los seeders se ubican en la carpetadatabase/seedsy puedes crear tantos como desees.

Cuando queremos crear un usuario tipo “admin” podemos hacerlo de forma manual en un seed, pero cuando queremos insertar muchos usuarios debe de existir una manera más agradable de lograrlo, ahí entraFaker.

Faker es un componente que genera datos para ti. De manera que con solo agregar el componente, hacer el llamado del mismo en el seed más unas simples líneas de códigos, podrás tener tantos datos como sean necesarios para evaluar tu aplicación correctamente.

Escribiendo seeders  ejecuta el

Comando 

**`php Artisan make:seeder UsersTableSeeder`**

Todos los seeders generados por el framework seran colocados en el directorio database/seeds

en el archivo te diriges a la función run  y escribes  los datos que deseas ingresar

 

![](../.gitbook/assets/image%20%288%29.png)

no olvidar usar el  facade DB **`use Illuminate\Support\Facades\DB;`**

**\`\`**

### Ejecutando seeders <a id="ejecutando-seeders"></a>

Una vez que hayas escrito tu seeder, puedes necesitar regenerar el cargador automático de Composer usando el comando `dump-autoload`:

```text
composer dump-autoload
```

Ahora puedes usar el comando Artisan `db:seed` para alimentar tu base de datos. De forma predeterminada, el comando `db:seed` ejecuta la clase `DatabaseSeeder`, la cual puede ser usada para ejecutar otras clases seeder. Sin embargo, puedes usar la opción `--class` para especificar que una clase seeder específica se ejecute individualmente:

![en el archivo DatabaseSeeder escribimos N seeder que creamos ](../.gitbook/assets/image%20%286%29.png)

    **``**

![](../.gitbook/assets/image%20%283%29.png)

```text
php artisan db:seed

php artisan db:seed --class=UsersTableSeeder
```

También puedes alimentar tu base de datos usando el comando `migrate:fresh`, el cual eliminará todas las tablas y volverá a ejecutar todas tus migraciones. Este comando es útil para reconstruir tu base de datos completamente:

```text
php artisan migrate:fresh --seed
```

