# Ejemplo: catálogo de libros

Este código XML Schema define la estructura y los tipos de datos del XML de ejemplo anterior. Define un elemento raíz llamado catalogo que contiene una secuencia de elementos libro. Cada elemento libro tiene un atributo id y lenguaje, y contiene elementos para titulo, autor, editorial, precio, codigo_ejemplo, y url. La estructura y tipos de datos de cada elemento y atributo están definidos en el código XML Schema.

## RELAX NG

Este código especifica que el elemento raíz es ***'catalogo'*** y que debe contener uno o más elementos ***'libro'***. Cada ***'libro'*** debe tener los atributos ***'id'*** y ***'lenguaje'***, y los elementos ***'titulo'***, ***'autor'***, **'editorial'***, ***'precio'***, ***'codigo_ejemplo'*** y ***'url'***. 

***'editorial'*** debe contener los elementos ***'nombre'*** y ***'año'***. 

***'precio'*** debe tener el atributo ***'moneda'*** y un valor numérico decimal. 

***'codigo_ejemplo'*** debe contener cualquier cadena de texto. 

***'url'*** debe contener una URI.
