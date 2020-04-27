# Metodos CRUD

los siguientes son códigos que se utilizan para la realización un **CRUD** , pero antes no se olvide usar el controlador de la clase en  controlador 

**insertar datos**

\*\*\*\*

```text
<form  method="POST" action="{{route('contacto.store')}}"  >
   @csrf  
```

```text
 public function store(Request $request)
    {
   //realizamos la insercion de los datos con ORM 
             
  $result =  Contact::create($request->all());
         
    return redirect()->route("contacto.index")->with('success','Satisfactorio!');
         enviamos mensaje flash 
    }
```

**Actualizar**

   

```text
<form  method="POST" action="{{route('contacto.update', $contacto->id)}}">
  @method("PUT")
  @csrf  
    
```



```text
 public function update(Request $request, $id)
    {

        buscamos el id si no lo encuentra envia error
        $solicitud = contact::findOrfail($id);
        $solicitud->fill($request->all());
          $solicitud->save();
      
      return redirect()->route("contacto.index")->with('warning','Editado Satisfactorio');
      enviamos mensaje flash 
    }
    
```

**Eliminar** 

 _crear una ruta personalizada._  **** y realizamos el llamado enviando el id a eliminar 

\*\*\*\*

```text
route::get('/contacto/{id}/destroy','ContactController@destroy')->name('contacto.destroy');
```

```text
<a href="{{route('contacto.destroy',$item->id)}}"
```



```text
public function destroy($id)
    {
        
   $delete = Contact::findOrFail($id);
  $delete->delete();
   return redirect()->route("contacto.index")->with('delete','Eliminado Satisfactorio');
        enviamos el mensaje flash

    }
```



