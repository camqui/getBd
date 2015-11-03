# Libreria getBd 
![](http://i.imgur.com/q2CBZ1t.png?1)

#### libreria basica para gestionar consultas a la base de dato.

------------------------------------------------------
 + Copyright by **FRANCISCO CAMPOS** 
 + Vercion: BETA
 + Licencia: OpenSource 
 + Contactar: <camqui2011@gmail.com>
 + [https://gitlab.com/franpc/getBd.git](http://)
 + Requicito: [Apache2 ,  php5 ]

------------------------------------------------------ 
[TOC]
Tiene soporte para: 

+ Mysql
+ Postgres
+ Help

******************************************************

### Extructura de la Libreria:

#### getBd:

    -class
        class_file.php
        class_mysql.php 
        class_postgre.php  
    -config
        config.php
    - README.md
    



### Descripcion de la Libreria:

------------------------------------------------------

**Class:** contiene las class necesaria para el manejo rapido de las consultas a la base de datos.

    - class_mysql.php:
Contiene las clases y metodos requerido el uso de Mysql.

    - class_postgre.php:
Contiene las clases y metodos requerido el uso de Postgres.

    - class_file.php:
Contiene las clases nesesarias para trabajos.  


+ Subida de Archivos al servidor.



**Config:** Contiene las class dode se crea la conexion a la base de datos, aqui configuraremos las variables de la conexion: root , localhost , password.

    - config.php:

## Funcionamiento:

Configuracion de las variables de conexión.

*config/config.php*
 
 **Class Mysql:**

 Inicializamos los valores en el  constructor de la clase.

    public function __construct()
    {  
        $this->localhost = 'nombre del host';
        $this->usuario = 'usuario del host';
        $this->password = 'clave del host';
        $this->bd = 'nombre de base de datos';
    }

**Class Postgres:**

 Inicializamos los valores en el  constructor de la clase.

    public function __construct()
    {  
        $this->localhost = 'nombre del host';
        $this->usuario = 'usuario del host';
        $this->password = 'clave del host';
        $this->bd = 'nombre de base de datos';
    }

Ejemplo de uso en Mysql:


**Archivo demo.php**
```
<?php

//Requerimos la clase para Mysql
require_once 'class/class_mysql.php';

//Instancisa del objeto para Mysql
 $con = new GetbdM();

?>

```


Ejemplo de uso en Postgres:


**Archivo demo.php**
```
<?php

//Requerimos la clase para Postgres
require_once 'class/class_postgre.php';

//Instancisa del objeto para Postgres
$con = new GetbdP();

?>
```

## getBd con Mysql

**Insertar registros en la base de datos:**

`save( sql )`

Este metodo recibe un parametro, la consulta SQL.

- **sql:**  consulta sql a insertar, Nota: la variable puede ser llamada de otra forma!

Retorna:

- **true:**  Si la consulta se realizo correctamente.
- **false:** Si la consulta no se realizo correctamente.
Con getBd es posible verificar el registro antes de ser insertado, todo en una sola linea de codigo.

Usamos el método: 

`check( [ 'tabla' , 'campos' , 'valor'] )`

- **tabla** : Nombre de la tabla donde sera verificado el registro.
- **campo**: Campos referencia para la condicion a cumplir.
- **valor**: Valor de verificacion de la condicion.

Retorna:

- **true**: Si existe el registro.
- **false**: No se encotro registro.

**Nota:** Uselo antes del metodo save()
Ejemplo:

    `obj->check( [ 'tabla' , 'campos' , 'valor'] )->save(sql)`

Archivo demo.php

```
<?php 

require_once 'class/class_mysql.php';


$con = new GetbdM();

$sql = "INSERT INTO tabla (campos) Values (valores)";

//verificador del registro

$con->check(['tabla' , 'campo' , 'valor'])->save($sql);

 if(!$con)
 {
   echo "Registro Insertado";
 }
 else
 {
   echo "Registro No Insertado";
 }
 
 
//Sin verificar registro

$con->save($sql);

 if(!$con)
 {
   echo "Registro Insertado";
 }
 else
 {
   echo "Registro No Insertado";
 }
?>
```


## Consultar registro de la base de datos

Para ello tenemos 2 metodos:

`find( parametro )`

+ Recibe un parametro que es la consulta SQL
+ Retorna **True:** Si hay registro
+ Retorna **False:**  Si no hay registro

`show()`

+ Retorna un Array Asociativo con los datos

## Consulta a la base de datos

```
 <?php
  require_once 'class/class_mysql.php';

  $obj = new GetbdM();
  
  $sql = "SELECT * FROM tabla ";

  $datos = $obj->find($sql)->show();

 //mostrando los registros
 
 foreach ($datos as $dato) {
    echo $dato['campo'] . "<br>";
 }
    
 ?>
```

## Consultar un registro unico en la  base de datos

Para ello tenemos el metodos:

`findOne( ['tabla' , 'campos', 'valor'] )`

+ Recibe un arreglo con 3 parametros 
+ Retorna **True:** Si hay registro
+ Retorna **False:**  Si no hay registro



+ Retorna un registro encontrado

## Consulta a la base de datos

```
 <?php
  require_once 'class/class_mysql.php';

  $obj = new GetbdM();
  
  $sql = "SELECT * FROM tabla ";

  $datos = $obj->findOne(['table' , 'id', 'valor']);

 //mostrando el registro

    print_r($dato );
 
    
 ?>
```

## Actualizar registro de la base de datos

Para ello tenemos el metodos:

`update( sql , 'string' )`

+ Recibe dos parametro que son: la consulta SQL , y la cadena 'update', para evitar error en la consulta. 
+ Retorna **True:** Si se actualizo el registro
+ Retorna **False:** Si no se actualizo el registro

```
 <?php
  require_once 'class/class_mysql.php';

 $obj = new GetbdM();
      
 $sql = "UPDATE  tabla SET campo = 'valor' where condicion";

  if ( !$con->update($sql , 'update')) 
  {
     echo "No! se actualizo el registro";
  }
  else
  {   
     echo "Registro actualizado";
  }

 ?>
```


## Eliminar registro de la base de datos

Para ello tenemos el metodos:

`remove(sql , string' )`

+ Recibe dos parametro que son : la consulta SQL , y la cadena 'delete', para evitar error en la consulta. 
+ Retorna **True:** Si se elimino el registro
+ Retorna **False:** Si no se elimino el registro

```
 <?php
  require_once 'class/class_mysql.php';

  $obj = new GetbdM();
  
  $sql = "DELETE FROM tabla WHERE condición";

  if($obj->remove($sql , 'delete'))
  {
  	echo "Registro eliminado";
  }
  else
  {
    echo "No! se elimino el registros";
  }

 ?>
```

## getBd  con  Postgres

El uso de getBd con Postgres es igual al funcionamiento con Mysql tenemos los mismo metodos. Solo cambia es el **include de la class**

```
<?php

//Requerimos la clase para Postgres
require_once 'class/class_postgre.php';

//Instancisa del objeto para Postgres
$con = new GetbdP();

?>
```

`save( parametro )` 

`find( parametro )`

`findOne( parametro )`

`show()`

`upadate( parametro , 'string' )`

`remove( parametro , 'string' )` 

**Nota:** 
 >puede ver los ejemplos de los metodos arriba.

## getBd subir archivos al servidor

Para ello tenemos la clase ` File()` que contiene los metodos:
    
`upFile()` 

* Recibe un primer parametro. file a subir.
* Recibe un segundo parametro el nombre de la carpeta donde se guarda el archivo.
* Retorna **Array:** con 2 valores el primero true , el sugundo la ruta final del archivo guardado.
* Retorna **False:** Si no se guardo el archivo.

>Array retornado:

```
 array respuesta = [ 'valid' => true , 'ruta'=> 'ruta del archivo' ];
```

Ejemplo de uso:

*index.html*

```
<!DOCTYPE html>

<html>
    <head>
    </head>
    <body>

        <form action="file.php" method="post" enctype="multipart/form-data">
         <input type="file" name="archivo" ></input><br>
         <input type="submit" value="Subir archivo"></input>
        </form>

    </body>

</html>
```

*demo.php*

```
 <?php 

require_once 'class/file.php';


$file = $_FILES['archivo'];//reciben el archivo

$archivo = new File(); //instancia de la clase

//usamos el metodo upFile(nombre del archivo , nombre de la carpeta)

$var = $archivo->upFile( $file , "nombre de la carpeta" );

if($var[0] == true){
    echo "Archivo subido";
    
    //ejemplo mostrando el archivo subido
    echo" <img src='$var[1]' /> ";
    
}else{
    echo "Error al subir archivo";
}

?>
```

## getBd con multiples archivos:

Para ello tenemos la clase ` File()` que contiene los metodos:
    
`upFiles()` 

* Recibe un primer parametro. file a subir.
* Recibe un segundo parametro el nombre de la carpeta donde se guarda el archivo.
* Retorna **Array:** con 2 valores el primero true , el sugundo la ruta final del archivo guardado.
* Retorna **Array:** con error  Si no se guardo el archivo.

```
array respuesta = {
  [0] => 'true',
  [1] => 'ruta del archivo guardado'
}

```

Ejemplo de uso:

*index.html*

```
<!DOCTYPE html>

<html>
    <head>
    </head>
    <body>

        <form action="file.php" method="post" enctype="multipart/form-data">
         <input type="file" name="archivo[]" multiple="multiple" ></input><br>
         <input type="submit" value="Subir archivo"></input>
        </form>

    </body>

</html>
```


*file.php*
```
 <?php 

require_once 'class/file.php'; //se puede usar con postgres


$file = $_FILES['archivo'];//reciben el archivo

$archivo = new File(); //instancia de la clase

//usamos el metodo upFiles(nombre del archivo , nombre de la carpeta)
//para la subida de varios archivos al servidor.

$var = $archivo->upFiles($file , "carpeta a guardar" );

echo "<pre>";

 print_r($var);//mostrando el resultado de la subida.

echo "</pre>";

?>
```


------------------------------------------------------
## Creditos:
 + Copyright by **FRANCISCO CAMPOS** 
 + Vercion: BETA
 + Licencia: OpenSource 
 + Contactar: <camqui2011@gmail.com>


[TOC]