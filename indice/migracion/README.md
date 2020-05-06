# las Migraciones

Las migraciones son como un control de versiones del estado de nuestras tablas. Están preparadas para ejecutarse en "ida y vuelta". Osea, podemos correr el sistema de migraciones para obtener la base de datos en su estado final, así como también podríamos volver hacia atrás, para recuperar cualquier estado de la base de datos hasta llegar al estado inicial, en el que se supone que no habría tabla alguna. 

Las migraciones están dentro de la carpeta database/migrations y en la instalación de base de Laravel ya incorporan un par de archivos de migraciones, por lo que podemos observar cómo se han construido. Son un par de archivos para creación de la tabla de usuarios "users" y la tabla "password\_resets", componentes del sistema de login de usuarios de Laravel.

### Generando migraciones <a id="generando-migraciones"></a>

Para crear una migración, usa el comando Artisan `make:migration`:

```text
php artisan make:migration create_users_table 
"siempre el nombre de la tabla en plurar"
```

La nueva migración estará ubicada en tu directorio `database/migrations`. Cada nombre de archivo de migración contiene una marca de tiempo la cual permite que Laravel determine el orden de las migraciones.

Las opciones `--table` y `--create` también pueden ser usadas para indicar el nombre de la tabla y si la migración estará creando una nueva tabla. Estas opciones rellenan previamente el archivo stub de migración generado con la tabla especificada:

```text
php artisan make:migration create_users_table --create=users

php artisan make:migration add_votes_to_users_table --table=users
```

Si prefieres especificar una ruta de directorio de salida personalizada para la migración generada, puedes usar la opción `--path` al momento de ejecutar el comando `make:migration`. La ruta de directorio dada debe ser relativa a la ruta de directorio base de tu aplicación.



### Estructura de migración <a id="estructura-de-migracion"></a>

Una clase de migración contiene dos métodos: `up` y `down`. El método `up` es usado para agregar nuevas tablas, columnas, o índices para tu base de datos, mientras el método `down` debería revertir las operaciones ejecutadas por el método `up`.

Dentro de ambos métodos puedes usar el constructor de esquema de Laravel para crear y modificar expresivamente las tablas. Para aprender sobre todos los métodos disponibles en el constructor `Schema`, [inspecciona su documentación](https://documentacion-laravel.com/migrations.html#creating-tables). Por ejemplo, este ejemplo de migración crea una tabla `flights`:

```text
<?php

use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateFlightsTable extends Migration
{
    /**
    * Run the migrations.
    *
    * @return void
    */
    public function up()
    {
        Schema::create('flights', function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->string('name');
            $table->string('airline');
            $table->timestamps();
        });
    }

    /**
    * Reverse the migrations.
    *
    * @return void
    */
    public function down()
    {
        Schema::drop('flights');
    }
}
```

### [\#](https://documentacion-laravel.com/migrations.html#ejecutando-migraciones)Ejecutando migraciones <a id="ejecutando-migraciones"></a>

Para ejecutar todas tus maravillosas migraciones, ejecuta el comando Artisan `migrate`:

```text
php artisan migrate
```



#### Revertir migraciones <a id="revertir-migraciones"></a>

Para revertir la operación de migración más reciente, puedes usar el comando `rollback`. Este comando reversa el último "lote" de migraciones, los cuales pueden incluir archivos de migración múltiples.

```text
php artisan migrate:rollback
```

Puedes revertir un número limitado de migraciones proporcionando la opción `step` al comando `rollback`. Por ejemplo, el siguiente comando revertirá los cinco "lotes" de migraciones más recientes:

```text
php artisan migrate:rollback --step=5
```

El comando `migrate:reset` revertirá todas las migraciones de tu aplicación:

```text
php artisan migrate:reset
```

Laravel usa el conjunto de caracteres `utf8mb4` por defecto, el cual incluye soporte para almacenar "emojis" en la base de datos. Si estás ejecutando una versión de MySQL más antigua que la versión 5.7.7 o más vieja que la versión 10.2.2 de MariaDB, puedes que necesites configurar manualmente la longitud de cadena predeterminada generada por las migraciones con el propósito de que MySQL cree los índices para estos. Puedes configurar esto ejecutando el método `Schema::defaultStringLength` dentro de tu `AppServiceProvider`:

```text
use Illuminate\Support\Facades\Schema;

/**
* Bootstrap any application services.
*
* @return void
*/
public function boot()
{
    Schema::defaultStringLength(191);
}
```

Alternativamente, puedes habilitar la opción `innodb_large_prefix` para tu base de datos. Debes referirte a la documentación de tu base de datos para conocer las instrucciones de cómo habilitar ésta apropiadamente.



#### Restricciones de clave foránea <a id="restricciones-de-clave-foranea"></a>

Laravel también proporciona soporte para la creación de restricciones de clave foránea, las cuales son usadas para forzar la integridad referencial a nivel de base de datos. Por ejemplo, vamos a definir una columna `user_id` en la tabla `posts` que referencia la columna `id` en una tabla `users`:

```text
Schema::table('posts', function (Blueprint $table) {
    $table->unsignedBigInteger('user_id');

    $table->foreign('user_id')->references('id')->on('users');
});
```

También puedes especificar la acción deseada para las propiedades "on delete" y "on update" de la restricción:

```text
$table->foreign('user_id')
      ->references('id')->on('users')
      ->onDelete('cascade');
```

