# Plantilla Blade

 Blade es un motor de plantillas simple y a la vez poderoso proporcionado por Laravel. A diferencia de otros motores de plantillas populares de PHP, Blade no te impide utilizar código PHP plano en sus vistas. De hecho, todas las vistas de Blade son compiladas en código PHP plano y almacenadas en caché hasta que sean modificadas, lo que significa que Blade no añade sobrecarga a tu aplicación. Los archivos de las vistas de Blade tienen la extensión `.blade.php` y son usualmente almacenados en el directorio `resources/views`

#### Definir un layout <a id="definir-un-layout"></a>

Dos de los principales beneficios de usar Blade son _la herencia de plantillas_ y _secciones_. Para empezar, veamos un ejemplo simple. Primero, vamos a examinar una página de layout "master". Ya que la mayoría de las aplicaciones web mantienen el mismo layout general a través de varias páginas, es conveniente definir este layout como una sola vista de Blade:

```text
<!-- Almacenado en resources/views/layouts/app.blade.php -->

<html>
    <head>
        <title>App Name - @yield('title')</title>
    </head>
    <body>
        @section('sidebar')
            This is the master sidebar.
        @show

        <div class="container">
            @yield('content')
        </div>
    </body>
</html>
```

Como puedes ver, este archivo contiene el marcado típico de HTML. Sin embargo, toma nota de las directivas `@section` y `@yield`. La directiva `@section`, como su nombre lo indica, define una sección de contenido, mientras que la directiva `@yield` es utilizada para mostrar el contenido en una sección determinada.

Ahora que hemos definido un layout para nuestra aplicación, vamos a definir una página hija que herede el layout.

#### [\#](https://documentacion-laravel.com/blade.html#extender-un-layout)Extender un layout <a id="extender-un-layout"></a>

Al definir una vista hija, utiliza la directiva de Blade `@extends` para indicar el layout que deberá "heredarse" en la vista hija. Las vistas que extiendan un layout de Blade pueden inyectar contenido en la sección del layout usando la directiva `@section`. Recuerda, como vimos en el ejemplo anterior, los contenidos de estas secciones se mostrarán en el layout usando `@yield`:

```text
<!-- Almacenado en resources/views/child.blade.php -->

@extends('layouts.app')

@section('title', 'Page Title')

@section('sidebar')
    @@parent

    <p>This is appended to the master sidebar.</p>
@endsection

@section('content')
    <p>This is my body content.</p>
@endsection
```

**@extends ``**

para indicar el layout que deberá "heredarse" en la vista hija. Las vistas que extiendan un layout de Blade pueden inyectar contenido en la sección del layout usando la directiva

**@section**





**@yield**



**@parent**

\*\*\*\*

**@include**

\*\*\*\*

### Mostrando datos <a id="mostrando-datos"></a>

Puedes mostrar datos pasados a tu vista de Blade al envolver la variable entre llaves. Por ejemplo, dada la siguiente ruta:

```text
Route::get('greeting', function () {
    return view('welcome', ['name' => 'Samantha']);
});
```

Puedes mostrar el contenido de la variable `name` de la siguiente manera:

```text
Hello, {{ $name }}.
```

No estás limitado a mostrar sólo el contenido de las variables pasadas a la vista. También puedes hacer echo al resultado de cualquier función de PHP. De hecho, puedes poner cualquier código PHP que desees dentro de la declaración echo de Blade:

```text
The current UNIX timestamp is {{ time() }}.
```

TIP

**Las declaraciones de Blade {{ }} son enviadas automáticamente mediante la función htmlspecialchars de PHP para prevenir ataques XSS.**

\*\*\*\*

**Mostrar datos no escapados**

De manera predeterminada, las declaraciónes `{{ }}` de Blade son enviadas mediante la función `htmlspecialchars` de PHP para prevenir ataques XSS. Si no deseas que tu información sea escapada, puedes utilizar la siguiente sintáxis:

```text
Hello, {!! $name !!}.
```

\*\*\*\*

