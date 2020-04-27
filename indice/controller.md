# Los Controladores

 Los controladores son un mecanismo que nos permite agrupar la lógica de peticiones HTTP relacionadas y de esta forma organizar mejor nuestro código. En esta quinta lección del **Curso de Laravel desde cero** aprenderemos a hacer uso de ellos y veremos además cómo las pruebas unitarias nos permiten verificar los cambios que introducimos en nuestro código de forma fácil y rápida.

### Controladores básicos <a id="controladores-basicos"></a>

#### [\#](https://documentacion-laravel.com/controllers.html#definiendo-controladores)Definiendo controladores <a id="definiendo-controladores"></a>

A continuación se muestra un ejemplo de una clase de controlador básica. Nota que el controlador extiende la clase de controlador base incluida con Laravel. La clase base proporciona unos cuantos métodos de conveniencia tal como el método `middleware`, el cual puede ser usado para conectar un middleware a acciones de controlador:

```text
<?php

namespace App\Http\Controllers;

use App\Http\Controllers\Controller;
use App\User;

class UserController extends Controller
{
    /**
    * Show the profile for the given user.
    *
    * @param  int  $id
    * @return View
    */
    public function show($id)
    {
        return view('user.profile', ['user' => User::findOrFail($id)]);
    }
}
```

Puedes definir una ruta a esta acción de controlador de esta forma:

```text
Route::get('user/{id}', 'UserController@show');
```

Ahora, cuando una solicitud coincide con la URI de la ruta especificada, se ejecutará el método `show` de la clase `UserController`. Los parámetros de ruta también se pasarán al método.



#### Controladores y espacios de nombres <a id="controladores-y-espacios-de-nombres"></a>

Es muy importante notar que no necesitamos especificar el espacio de nombre completo del controlador al momento de definir la ruta del controlador. Debido a que el `RouteServiceProvider` carga sus archivos de ruta dentro de un grupo de ruta que contiene el espacio de nombre, solamente necesitaremos la porción del nombre de la clase que viene después de la porción `App\Http\Controllers` del espacio de nombre.

Si eliges anidar tus controladores dentro del directorio `App\Http\Controllers`, usa el nombre de clase específico relativo al espacio de nombre raíz `App\Http\Controllers`. Así, si tu clase de controlador completa es `App\Http\Controllers\Photos\AdminController`, deberías registrar rutas al controlador de esta forma:

```text
Route::get('foo', 'Photos\AdminController@method');
```



### Controladores de recursos <a id="controladores-de-recursos"></a>

El enrutamiento de recurso de Laravel asigna las rutas típicas "CRUD" a un controlador con una sola línea de código. Por ejemplo, puedes desear crear un controlador que maneje todas las solicitudes HTTP para "photos" almacenadas por tu aplicación. Usando el comando Artisan `make:controller`, podemos crear fácilmente tal controlador:

```text
php artisan make:controller PhotoController --resource
'primera letra mayusculay finalizando con controller'
```

Este comando creará un controlador en `app/Http/Controllers/PhotoController.php`. El controlador contendrá un método para cada una de las operaciones de recursos disponibles.

Seguidamente, puedes registrar una ruta de recurso genérica al controlador:

```text
Route::resource('photos', 'PhotoController');
```

Esta declaración de ruta única crea varias rutas para manejar una variedad de acciones del recurso. El controlador generado ya tendrá los métodos separados para cada una de las acciones, incluyendo comentarios que te informan de los verbos HTTP y URIs que manejan.

Puedes registrar muchos controladores de recursos a la vez pasando un arreglo al método `resources`:

```text
Route::resources([
    'photos' => 'PhotoController',
    'posts' => 'PostController'
]);
```



**Especificando el modelo del recurso**

Si estás usando el enlace de modelo de ruta \(route model binding\) y deseas que los métodos del controlador de recursos declaren el tipo de una instancia de modelo, puedes usar la opción `--model` al momento de generar el controlador:

```text
php artisan make:controller PhotoController --resource --model=Photo
```

**\#Suplantar los métodos de formulario**

Debido a que los formularios no pueden hacer solicitudes `PUT`, `PATCH`, o `DELETE`, necesitarás agregar un campo `_method` oculto para suplantar estos verbos HTTP. La directiva de Blade `@method` puede crear este campo para ti:

```text
<form action="/foo/bar" method="POST">
    @method('PUT')
</form>
```

