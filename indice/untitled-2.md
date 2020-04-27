# Validacion Formulario

### Validación de formularios clase Request: Laravel 5

Laravel ofrece atajos útiles, herramientas y componentes para ayudarte a conseguir el éxito en tus proyectos basados en web, si no que también intenta arreglar alguna de las flaquezas de PHP.

Nosotros podemos generar un validador para cada formulario de forma muy sencilla haciendo uso de php artisan make:request nombre, de esta forma, laravel creará un nuevo archivo con nuestro nombre ubicado en la carpeta app\Http\Requests



#### Creando solicitudes de formulario \(form request\) <a id="creando-solicitudes-de-formulario-form-request"></a>

Para escenarios de validación más complejos, puede que desees crear una "solicitud de formulario \(form request\)". Las Form Request son clases de solicitud personalizadas que contienen la lógica de validación. Para crear una clase de Form Request, usa el comando de CLI de Artisan `make:request`:

```text
php artisan make:request StoreBlogPost
 php artisan make:request UpdateBlogPost
```

se recomienda crear un archivo validar el ingreso y actualización 

la clase generada será colocada en el directorio `app/Http/Requests`. Si este directorio no existe, será creado cuando ejecutes el comando `make:request`. Agreguemos unas cuantas reglas de validación al método `rules`:



_recordar que en la función **authorize** debe cambiarse a true._

```text
/**
* Get the validation rules that apply to the request.
*
* @return array
*/
public function rules()
{
    return [
        'title' => 'required|unique:posts|max:255',
        'body' => 'required',
    ];
}
```



**Obteniendo todos los mensajes de error para todos los campos**

Para obtener un arreglo de todos los mensajes para todos los campos, usa el método `all`:

```text
foreach ($errors->all() as $message) {
    //
}
```

_**`la variable $errors se cargara automáticamente en la vista`**_ 

**\#Determinando si existen mensajes para un campo**

El método `has` puede ser usado para determinar si existe algún mensaje de error para un campo dado:

```text
if ($errors->has('email')) {
    //
}
```



**Forzando una regla unique para ignorar un ID dado:**

_esencial cuando vamos actualizar una informacion y le decimos que esta columna no se valide con su mismo  por que encontrara su mismo ID  y presentara problemas._

Algunas veces, puedes desear ignorar un ID dado durante la verificación de unicidad. Por ejemplo, considera una pantalla "update profile" que incluya el nombre del usuario, dirección de correo electrónico, y ubicación. Posiblemente, querrás verificar que la dirección de correo electrónico es única. Sin embargo, si el usuario solamente cambia el campo nombre y no el campo con el correo electrónico, no quieres que un error de validación sea lanzado porque el usuario ya es el propietario de la dirección de correo electrónico.

Para instruir al validador para que ignore el ID del usuario, usaremos la clase `Rule` para definir fluidamente la regla. En este ejemplo, también especificaremos las reglas de validación como un arreglo en lugar de usar el carácter `|` para delimitar las reglas:

```text
use Illuminate\Validation\Rule;

Validator::make($data, [
    'email' => [
        'required',
        Rule::unique('users')->ignore($this->user->id),
    ],
]);
```

**Funciones** 

```
recibira numeros y el select no aceptara el 1er campo
'dni_id'=> 'required | integer | not_In:0', 

el campo es requerido
'nombre_contacto' =>  'required',


```

