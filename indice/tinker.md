# Consola Tinker

Tinker viene con laravel por defecto, este nos permite interactuar con toda la aplicación que estemos creando a través de la linea de comandos, esto es buen de echo es muy bueno.

Genial, pero que es realmente. Bueno tinker esta realizado con psysh, este es una runtime developer console, interactive debugger and REPL for PHP. De lo cual tinker toma la parte REPL \(**bucle Lectura-Evaluación-Impresión**\) para hacer consultas rápidas sin tener que correr el programa entero.

### ¿Como uso Tinker?

para correr tinker solo necesita correr el siguiente comando en consola:

**`php artisan tinker`**

 puede usar la consola de windows

Una vez dentro de tinker puede hacer consultas incluso insertar datos a través de esta, este resulta efectivo para testear por ejemplo una consulta antes de ir escribirla en el controlador levantar **php artisan serve** y todo eso resulta muy fácil correr el comando aquí.

Ahora corramos alguna consulta en thinker, para este ejemplo usare la misma base de datos que use en la introducción a eloquent. Por tanto tendre un Model Cliente y la base de datos example.

![](../.gitbook/assets/image%20%287%29.png)

los datos que tengo son los siguientes.

Casi todo es aplicable en tinker, así que veamos unos ejemplos de eloquent.

probemos traer todos los clientes con todos sus datos

**`\App\Cliente::all();`**

El resultado sera el siguiente:



```text
>>> \App\Cliente::all();
=> Illuminate\Database\Eloquent\Collection {#2950
     all: [
       App\Cliente {#2951
         id: 1,
         nombre: "Jose",
         apellido: "Garcia",
         telefono: "09737483",
         direccion: "Peru 1978",
       },
       App\Cliente {#2952
         id: 2,
         nombre: "Maria",
         apellido: "Gonzales",
         telefono: "09987624",
         direccion: "Peru 1978",
       },
       App\Cliente {#2953
         id: 3,
         nombre: "Jose",
         apellido: "Garcia",
         telefono: "09737483",
         direccion: "Peru 1978",
       },
       App\Cliente {#2954
         id: 4,
         nombre: "Maria",
         apellido: "Gonzales",
         telefono: "09987624",
         direccion: "Peru 1978",
       },
       App\Cliente {#2955
         id: 5,
         nombre: "Marcos",
         apellido: "Aloicio",
         telefono: "090584152",
         direccion: "Ansina 901",
       },
       App\Cliente {#2956
         id: 6,
         nombre: "Lorenzo",
         apellido: "Esquer",
         telefono: "09987633",
         direccion: "Ansina 901",
       },
     ],
   }
```



