# Rutas

 Las rutas en Laravel son las responsables de indicar el procedimiento que debe seguir nuestra aplicación, es decir, si nosotros pedimos la ruta  ****queremos que nos liste todos los posts. Si queremos el post 1, tendremos una ruta como por ejemplo **/post/1**.

tanto las peticiones GET como POST las podemos manejar con las rutas y controladores. 

 también Las rutas de Laravel más básicas aceptan una URL y una `Closure`, proporcionando un método muy fácil y expresivo de definición de rutas:

```text
Route::get('foo', function () {
    return 'Hello World';
});
```

Todas las rutas de Laravel están definidas en tus archivos de ruta, los cuales están localizados en el directorio `routes`. Estos archivos son cargados automáticamente por el framework. El archivo `routes\web.php` define rutas que son para tu interface web. Estas rutas son asignadas al grupo de middleware `web`, el cual proporciona características como estado de sesión y protección CSRF. Las rutas en `routes\api.php` son independientes de estado y son asignadas al grupo de middleware `api`.

Para las principales aplicaciones, empezarás definiendo rutas en tu archivo `routes/web.php`. Las rutas definidas en `routes/web.php` pueden ser accedidas colocando la URL de la ruta definida en tu navegador. Por ejemplo, puede acceder a la siguiente ruta al navegar a `http://your-app.dev/user` en tu navegador:

```text
Route::get('/user', 'UserController@index');
```

 Las rutas definidas en el archivo `routes/api.php` son agrupadas dentro de un grupo de ruta por el `RouteServiceProvider`.Dentro de este grupo, el prefijo de URI `/api` es aplicado automáticamente de modo que no es necesario aplicarlo manualmente en todas las rutas en el archivo. Puedes modificar el prefijo y otras opciones de grupos de ruta al modificar tu clase `RouteServiceProvider`.

**Métodos disponibles del enrutador**

El enrutador permite que registres rutas que responden a cualquier verbo HTTP:

```text
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
```

 Algunas veces puede que necesites registrar una ruta que responda a verbos HTTP múltiples. Puedes hacerlo usando el método `match`. También, puedes incluso registrar una ruta que responda a todos los verbos HTTP usando el método `any`:



```text
Route::match(['get', 'post'], '/', function () {
    //
});

Route::any('/', function () {
    //
});
```



**Protección CSRF**

Cualquiera de los formularios HTML que apunten a rutas `POST`, `PUT`, or `DELETE` que sean definidas en el archivo de rutas `web` deberían incluir un campo de token CSRF. De otra manera, la solicitud será rechazada. Puedes leer más sobre protección CSRF en la documentación de CSRF:

```text
<form method="POST" action="/profile">
    {{ csrf_field() }}
    ...
</form>
```

#### [\#](https://documentacion-laravel.com/routing.html#redireccionar-rutas)Redireccionar rutas <a id="redireccionar-rutas"></a>

Si estás definiendo una ruta que redirecciona a otra URI, puedes usar el método `Route::redirect`. Este método proporciona una forma abreviada conveniente de modo que no tengas que definir una ruta completa o de controlador para ejecutar una redirección básica:

```text
Route::redirect('/here', '/there');
```

Por defecto, `Route::redirect` retorna un código de estado `302`. Puedes personalizar el código de estado usando el tercer parámetro opcional:

```text
Route::redirect('/here', '/there', 301);
```

Puedes usar el método `Route::permanentRedirect` para retornar un código de estado `301`:

```text
Route::permanentRedirect('/here', '/there');
```

#### [\#](https://documentacion-laravel.com/routing.html#rutas-de-vista)Rutas de vista <a id="rutas-de-vista"></a>

Si tu ruta necesita solamente devolver una vista, puedes usar el método `Route::view`. Igual que el método `redirect`, este método proporciona una forma abreviada básica de modo que no tengas que definir una ruta completa o de controlador. El método `view` acepta una URI como su primer argumento y un nombre de vista como su segundo argumento. Además, puedes proporcionar una arreglo de datos para pasar a la vista como un tercer argumento opcional:

```text
Route::view('/welcome', 'welcome');

Route::view('/welcome', 'welcome', ['name' => 'Taylor']);
```

### [\#](https://documentacion-laravel.com/routing.html#parametros-de-ruta)Parámetros de ruta <a id="parametros-de-ruta"></a>

#### [\#](https://documentacion-laravel.com/routing.html#parametros-requeridos)Parámetros requeridos <a id="parametros-requeridos"></a>

Con frecuencia necesitarás capturar segmentos de la URI dentro de tu ruta. Por ejemplo, puedes necesitar capturar un ID de usuario de la URL. Puedes hacer eso al definir los parámetros de ruta:

```text
Route::get('user/{id}', function ($id) {
    return 'User '.$id;
});
```

Puedes definir tantos parámetros de ruta como requieras para tu ruta:

```text
Route::get('posts/{post}/comments/{comment}', function ($postId, $commentId) {
    //
});
```

Los parámetros de ruta siempre son encerrados dentro de `{}`, deberían consistir de caracteres alfabéticos y no pueden contener un caracter `-`. En lugar de usar el caracter `-`, use el guión bajo \(`_`\). Los parámetros de ruta son inyectados dentro de las funciones de retorno de ruta / controlador en base a su orden - los nombres de los argumentos de la función de retorno / controlador no importan.

#### [\#](https://documentacion-laravel.com/routing.html#parametros-opcionales)Parámetros opcionales <a id="parametros-opcionales"></a>

Ocasionalmente puede que necesites especificar un parámetro de ruta, pero que aparezca como un parámetro opcional de esa ruta. Puedes hacer eso al colocar un signo de interrogación `?` después del nombre del parámetro. Asegúrate de dar un valor por defecto a la variable correspondiente de la ruta.

```text
Route::get('user/{name?}', function ($name = null) {
    return $name;
});

Route::get('user/{name?}', function ($name = 'John') {
    return $name;
});
```

#### [\#](https://documentacion-laravel.com/routing.html#restricciones-con-expresiones-regulares)Restricciones con expresiones regulares <a id="restricciones-con-expresiones-regulares"></a>

Puedes restringir el formato de tus parámetros de ruta usando el método `where` en una instancia de ruta. El método `where` acepta el nombre del parámetro y una expresión regular que defina cómo el parámetro debería estar conformado:

```text
Route::get('user/{name}', function ($name) {
    //
})->where('name', '[A-Za-z]+');

Route::get('user/{id}', function ($id) {
    //
})->where('id', '[0-9]+');

Route::get('user/{id}/{name}', function ($id, $name) {
    //
})->where(['id' => '[0-9]+', 'name' => '[a-z]+']);
```



### Rutas nombradas <a id="rutas-nombradas"></a>

Las rutas nombradas permiten la generación de URLs o redirecciones para rutas específicas de una forma conveniente. Puedes especificar un nombre para una ruta al encadenar el método `name` en la definición de la ruta:

```text
Route::get('user/profile', function () {
    //
})->name('profile');
```

También puedes especificar los nombes de ruta para acciones de controlador:

```text
Route::get('user/profile', 'UserController@showProfile')->name('profile');
```

**\#Generación de URLs para las rutas nombradas**

Una vez que has asignado un nombre a una ruta dada, puedes usar el nombre de la ruta cuando estás generando URLs o redireccionas por medio de la función `route` global:

```text
// Generating URLs...
$url = route('profile');

// Generando Redirecciones...
return redirect()->route('profile');
```

Si la ruta nombrada posee parámetros, puedes pasar los parámetros como el segundo argumento de la función `route`. Los parámetros dados serán insertados automáticamente dentro de la URL en sus posiciones correctas:

```text
Route::get('user/{id}/profile', function ($id) {
    //
})->name('profile');

$url = route('profile', ['id' => 1]);
```

Si pasas parámetros adicionales en el arreglo, estos pares clave / valor serán automáticamente agregados a la cadena de consulta generada de la URL:

```text
Route::get('user/{id}/profile', function ($id) {
    //
})->name('profile');

$url = route('profile', ['id' => 1, 'photos' => 'yes']);

// /user/1/profile?photos=yes
```



