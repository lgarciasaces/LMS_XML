# Ejemplo: Catálogo de libros

**Índice**
- [XML del catálogo de libros](#xml)
- [Comentarios en DTD, XML Schema y RELAX NG](#comentarios)
- [Código DTD](#dtd)
- [Código XML Schema](#xsd)
- [Código RELAX NG](#rng)

## XML del catálogo de libros <a name="xml"></a>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE catalogo SYSTEM "catalogo.dtd">
<catalogo>
  <!-- Este es un comentario -->
  <libro id="b001" lenguaje="JavaScript">
    <titulo>Eloquent JavaScript</titulo>
    <autor>Marijn Haverbeke</autor>
    <editorial>
      <nombre>Marijn Haverbeke</nombre>
      <año>2018</año>
    </editorial>
    <precio moneda="Euro">0</precio>
    <codigo_ejemplo><![CDATA[
      <script>
        function showMessage() {
          alert('Hello, world!');
        }
      </script>
    ]]></codigo_ejemplo>
    <url>https://eloquentjs-es.thedojo.mx/Eloquent_JavaScript.pdf</url>
  </libro>
  <libro id="b002" lenguaje="Java">
    <titulo>Curso de programación Java </titulo>
    <autor>Mariona Nadal</autor>
    <editorial>
      <nombre>ANAYA MULTIMEDIA</nombre>
      <año>2021</año>
    </editorial>
    <precio moneda="Euro">29,95</precio>
    <codigo_ejemplo><![CDATA[
        public class HolaMundo {
           public static void main(String[] args) {
              System.out.println("¡Hola, mundo!");
           }
        }
    ]]></codigo_ejemplo>
  </libro>
  <libro id="b003" lenguaje="HTML">
    <titulo>Guía HTML5. El presente de la web</titulo>
    <autor>John Freddy Vega &amp; Christian Van Der Henst</autor>
    <editorial>
      <nombre>Cristalab &amp; Maestros del web</nombre>
      <año>2011</año>
    </editorial>
    <precio moneda="Euro">5,45</precio>
    <codigo_ejemplo><![CDATA[
        <DOCTYPE html>
        <html lang="es">
            <head>
                <meta charset="utf-8"/>
                <title>Lección 2 de HTML5</title>
                <link rel="stylesheet" type="text/css" href="css/estilos.css">
            </head>
            <body>
                <header>
                    <h1>Lección 2 de HTML5</h1>
                <nav>
                    <ul>
                        <li><a href="#">Inicio</a></li>
                        <li><a href="#">Programas</a></li>
                    </ul>
                </nav>
                </header>
                <section>
                    <article>
                        <h2>Titulo del articulo</h2>
                        <p>Aqui va el artículo</p>
                        <img src="images/logo.png">             
                    </article>
                </section>
                <aside>
                    <h2>ASIDE</h2>
                    <p>Puede haber mas de uno, y se les da formato diferente asignándoles ID o CLASS con CSS</p>
                </aside>
                <footer>
                    <h2>FOOTER</h2>
                    <p>Aqui todo el contenido del footer</p>
                </footer>
            </body>
        </html>
     ]]></codigo_ejemplo>
  </libro>
</catalogo>
```
***

## Comentarios en DTD, XML Schema y RELAX NG <a name="comentarios"></a>

Los comentarios en **DTD** se escriben entre `<!--` y `-->`.
```
<!-- Este es un comentario en DTD -->
```

En **XML Schema**, los comentarios se escriben entre `<!--` y `-->`, al igual que en DTD.
```
<!-- Este es un comentario en DTD -->
```

En **RELAX NG**, los comentarios se escriben entre `##` y `##`. Por ejemplo:

```
## Este es un comentario en RELAX NG ##

```

*** 

## Código DTD <a name="dtd"></a>

```
<!ELEMENT catalogo (libro+)>
<!ELEMENT libro (titulo, autor, editorial, precio, codigo_ejemplo, url)>
<!ATTLIST libro
          id CDATA #REQUIRED
          lenguaje CDATA #REQUIRED>
<!ELEMENT titulo (#PCDATA)>
<!ELEMENT autor (#PCDATA)>
<!ELEMENT editorial (nombre, año)>
<!ELEMENT nombre (#PCDATA)>
<!ELEMENT año (#PCDATA)>
<!ELEMENT precio (#PCDATA)>
<!ATTLIST precio
          moneda CDATA #REQUIRED>
<!ELEMENT codigo_ejemplo (#PCDATA)>
<!ELEMENT url (#PCDATA)>

```

Este DTD define los elementos y atributos que pueden aparecer en el documento XML. 

También establece las reglas de estructura para cada elemento, como qué elementos deben estar contenidos dentro de otros elementos y cuántas veces pueden aparecer. 

Por ejemplo, el elemento `catalogo` debe contener uno o más elementos `libro`, mientras que el elemento `libro` debe contener exactamente un elemento `titulo`, un elemento `autor`, un elemento `editorial`, un elemento `precio`, un elemento `codigo_ejemplo`, y un elemento `url`. Además, el atributo `id` es requerido y el atributo `lenguaje` es requerido para el elemento `libro`, mientras que el atributo `moneda` es requerido para el elemento `precio`.


***

## Código XML Schema <a name="xsd"></a>

```
<?xml version="1.0"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <xs:element name="catalogo">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="libro" maxOccurs="unbounded">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="titulo" type="xs:string"/>
              <xs:element name="autor" type="xs:string"/>
              <xs:element name="editorial">
                <xs:complexType>
                  <xs:sequence>
                    <xs:element name="nombre" type="xs:string"/>
                    <xs:element name="año" type="xs:gYear"/>
                  </xs:sequence>
                </xs:complexType>
              </xs:element>
              <xs:element name="precio">
                <xs:complexType>
                  <xs:simpleContent>
                    <xs:extension base="xs:decimal">
                      <xs:attribute name="moneda" type="xs:string" use="required"/>
                    </xs:extension>
                  </xs:simpleContent>
                </xs:complexType>
              </xs:element>
              <xs:element name="codigo_ejemplo" type="xs:string"/>
              <xs:element name="url" type="xs:anyURI"/>
            </xs:sequence>
            <xs:attribute name="id" type="xs:string" use="required"/>
            <xs:attribute name="lenguaje" type="xs:string" use="required"/>
          </xs:complexType>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>

</xs:schema>

```

Este código XML Schema define la estructura y los tipos de datos del XML de ejemplo anterior. 

Define un elemento raíz llamado `catalogo` que contiene una secuencia de elementos `libro`. 

Cada elemento `libro` tiene un atributo `id` y `lenguaje`, y contiene elementos para `titulo`, `autor`, `editorial`, `precio`, `codigo_ejemplo`, y `url`. 

La estructura y tipos de datos de cada elemento y atributo están definidos en el código XML Schema.


***

## Código RELAX NG <a name="rng"></a>


```
default namespace = ""
element catalogo {
  element libro {
    attribute id {xs:string},
    attribute lenguaje {xs:string},
    element titulo {xs:string},
    element autor {xs:string},
    element editorial {
      element nombre {xs:string},
      element año {xs:integer}
    },
    element precio {
      attribute moneda {xs:string},
      xs:decimal
    },
    element codigo_ejemplo {
      xs:string
    },
    element url {xs:anyURI}
  }
}

```

Este código especifica que el elemento raíz es `catalogo` y que debe contener uno o más elementos `libro`. 

Cada `libro` debe tener los atributos `id` y `lenguaje`, y los elementos `titulo`, `autor`, `editorial`, `precio`, `codigo_ejemplo` y `url`. `editorial` debe contener los elementos `nombre` y `año`. `precio` debe tener el atributo `moneda` y un valor numérico decimal. `codigo_ejemplo` debe contener cualquier cadena de texto. `url` debe contener una URI.

