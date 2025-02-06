# Introducción

## Indice

- [Introducción](#introducción)
  - [Indice](#indice)
  - [Parciales](#parciales)
  - [Información Extra](#información-extra)
- [Clase 1 - Introducción DER y DER Extendido](#clase-1---introducción-der-y-der-extendido)
  - [Definición y Elementos](#definición-y-elementos)
  - [Dominio](#dominio)
  - [Clasificación de los Atributos](#clasificación-de-los-atributos)
  - [Identificador Unico (ID)](#identificador-unico-id)
  - [Relaciones](#relaciones)
  - [Opcionalidad](#opcionalidad)
  - [Entidades Fuertes y Debiles](#entidades-fuertes-y-debiles)
  - [Jerarquías](#jerarquías)
  - [Equivalencia de Relación Ternaria y Binarias](#equivalencia-de-relación-ternaria-y-binarias)
  - [Relaciones Transitivas](#relaciones-transitivas)
- [Clase 2 - Practica DER](#clase-2---practica-der)
- [Clase 3](#clase-3)
- [Clase 4](#clase-4)
- [Clase 5](#clase-5)
- [Clase 6](#clase-6)
- [Clase 7](#clase-7)
- [Clase 8](#clase-8)
- [Clase 9](#clase-9)
- [Clase 10](#clase-10)
- [Clase 11](#clase-11)

## Parciales

- 17/02 - 1° Parcial
- 05/03 - 2° Parcial
- 07/03 - Recuperatorio

## Información Extra

- **Profesores:** Agustin Gustavo y Crespo Natalia
- **Alumno:** Tiago Pujia
- **Comisión:** 1949 (verano, turno noche)
- **Fecha Inicio:** 03/02/2024
- **[Clases Grabadas](https://youtube.com/playlist?list=PLENvh_JZMnA7iPKJ3eZ-CZTfpCzVHT_yO&si=hLSYSkpMDpC3XZmM)**
- **[Apunte(este mismo)](https://github.com/Tiago-Pujia/Base-De-Datos)**

---

# Clase 1 - Introducción DER y DER Extendido

## Definición y Elementos

DER (diagrama de entidad relacion), representa con diagramas las base de datos. Es recomendado hacer uso de la herramienta [erdplus](erdplus.com).

- **Entidad**: Cosa/objeto abstraido y distinguido por cualidades (alumno, clase, empleado, etc...), debe englobar varias cualidades. Se representa por un cuadrado. En SQL equivaldria a una tabla.
- **Atributo**: Describe caracteristicas de la entidad (persona -> nombre, apellido, edad), el nombre debe ser representativo (como las variables de un lenguaje). Se representa por una elipse.En SQL equivaldria a las columnas de una tabla.
- **Relación**: Asocia las entidades entre sí, es una forma de conectarlas. Se representa po un rombo.
- **Registro**: Cada registro representa los valores de cada entidad, teniendo en cuenta los atributos

![der](imgs/clase-1/der.png)

## Dominio

El dominio (al igual que el analisis matematico) define el conjunto de valores que estan permitidos en los atributos. Por ejemplo, la edad entre 18 y 65, el legajo debe ser numerico, etc...

## Clasificación de los Atributos

- **Simple o Compuesto**: 

Los _simples_ son aquellos que no son divisibles en sub-atributos, por ejemplo la edad. Los _compuestos_ son lo divisibles como por ejemplo el domicilio -> Calle, Nro, Depto

![](imgs/clase-1/atributos-clasificaciones/compuesto.png)

- **Monovaluado ó Multivaluado**:

Los _monovaluado_ poseen un unico valor. Mientras que el _multivaluado_ puede contener varios valores, se represente con otra elipse superior.

![](imgs/clase-1/atributos-clasificaciones/multivaluado.png)

- **No derivado ó Derivado/Calculable**:

Los no derivados no pueden calcularse. Mientras que el valuado se calcula apartir de otro/s atributos, por ejemplo la edad apartir de una fecha. El derivado se representa con un borde en rallas.

![](imgs/clase-1/atributos-clasificaciones/derivado.png)

- **No Complejo ó Complejo**:

Los complejos son atributos compuestos y multivaluado.

![](imgs/clase-1/atributos-clasificaciones/complejo.png)

- **Nulo/Opcional ó No Nulo/Obligatorio**:

Los atributos pueden o no aceptar valores (nulos), según como se diseñe el atributo. 

<!-- - **Clave ó No Clave**: -->

## Identificador Unico (ID)

El ID es un atributo que representa al registro. Si se quiere hacer un llamado del registro, se puede optar por utilizar el ID por cuestiones de eficiencia en la programación. Se representa con un subrayado al nombre del atributo. 

Presenta caracteristicas como unico, no nulo, inmutable (no cambiar), puede ser alfanumerico o numerico, en la mayoria de casos es autoincremental si es numerico (ej: en cada registro nuevo automaticamente incrementa 1, 2, 3...)

![](imgs/clase-1/atributos-clasificaciones/id.png)

## Relaciones

Las relaciones establecen como se asocian las entidades. Se hace uso del teorema de conjuntos. 

![](imgs/clase-1/relacion.png)

> **Restricción de Cardinalidad**
> 
> La cardinalidad se refiere ala cantidad de instancias que pueden vincularse a una relación. Esta puede ser de diferentes tipos:
> 
> - **Uno a uno (1->1)**: Un registro de la primera tabla le corresponde como máximo un registro en la segunda tabla, y viceversa.
> 
> - **Uno a muchos (1->N)**: Un registro de la primera tabla le pueden corresponder muchos registros en la segunda tabla, pero cada registro de la segunda tabla solo tiene un registro asociado en la primera tabla.
> 
> - **Muchos a uno (N->1)**: Muchos registros de la primera tabla pueden estar asociados a un solo registro de la segunda tabla.
>
> - **Muchos a muchos (N->N)**: Muchos registros de la primera tabla pueden estar relacionados con muchos registros de la segunda tabla, y viceversa.
> 
> En el DER se debe indicar al lado de cada entidad el tipo de Cardinalidad. Ejemplo:
> 
> ![](imgs/clase-1/Cardinalidad.png)

> **Restricción de Participación**
> 
> Indica si es necesario que cada registro este relacionado si o si con otra entidad, o no.
> 
> - **Total**: Todos los elementos de la entidad deben participar en la relación
> - **Parcial** No todos los elementos de la entidad deben participar
> 
> Por ejemplo: En la primera imagen se ve que la entidad "profesor" tiene asignado todos los registros, por lo que es parcial. A lo contrario de la entidad "Alumno" en cual hay registros (A4) sin vinculo, por lo que es parcial.

> **Grado**
> 
> El grado indica la cantidad de participantes de una relación. Puede ser unaria, binaria o ternaria, aunque la ternaria es raro que ocurra.

## Opcionalidad

Restricción de participación es parte de la opcionalidad sobre la relación de los registros. Para indicar si es obligatorio en una entidad se utiliza doble linea en el conector, para la opcionalidad se utiliza una circunferencia.

![](imgs/clase-1/Opcionalidad.png)

De todas maneras, no es comun indicar la opcionalidad en el DER. Debido a que no influye en el Modelo Relacional/Diseño.

## Entidades Fuertes y Debiles

Las _entidades debiles_ son aquellas que no poseen un ID propio. Por lo tanto, necesitan hacer uso de otras entidades (_fuertes_) para diferenciar los registros y realizar llamados a los mismos.

![](imgs/clase-1/Entidad-Debil-Fuerte.png)

Su participación es total y no puede ser tipo N. Las debiles se identifican con un doble borde. 

## Jerarquías

Hay dos tipos de jerarquias:

> **Jerarquía de Generalización**
> 
> <!-- 
> Nace abajo y la generalizo; se tiene entidades distintas con cosas en comun y se genera una entidad madre que agrupa los atributos comunes
> -->
> 
> Comienza desde abajo agrupando las entidades con caracteristicas en comun, para ser englobado por una entidad madre; similar a obtener el factor comun. Se utiliza la forma geometrica hexágono con lados extendidos para indicar la Jerarquía.
> 
> Las entidades "hijos" heredan los atributos de la entidad "madre". Un registro pertenece siempre al madre y debe participar en una entidad hijo (_partición total_) y solo en uno (_sin solapamiento_).
> 
> ![](imgs/clase-1/Jerarquia-Generalizacion.png)
> 
> En este caso, todo vehiculo tendra si o si los atributos "patente" y "año fabricacion". Pertenecera a alguna de las entidades "Camion", "moto" o "auto", pero nunca dos o más a la vez.

> **Jerarquía de Subconjuntos**
> 
> Comparte similitudes con el generalizado, se lee de abajo hacia arriba y sigue agrupando entidades. Pero ya no tiene la forma geometrica como union, se utilizan flechas directamente.
> 
> Las entidades hijos siguen herando los atributos de la madre. Pero ahora, un registro puede pertener a ninguno (_partición parcial_), uno o todos a la vez (_solapamiento_).
> 
> ![](imgs/clase-1/Jerarquia-Subconjuntos.png)
> 
> En este caso, un alumno puede ser extranjero o becado, puede ser ninguna de las dos o ambas a la vez.

## Equivalencia de Relación Ternaria y Binarias

## Relaciones Transitivas

Hay que tener cuidado con las relaciones que se crean, la creación de cada una es equivalente a que se le haga mayor mantenimiento a la base de datos, por lo que se debe crear lo minimo indispensable. Por ejemplo:

> ![](imgs/clase-1/relacion-redundante-1.png)
> 
> En esta imagen se quiere consulta en que pais estudia el alumno. La solución erronea seria crear una relación entre ambas entidades, cuando se puede resolver haciendo un llamado a alumno -> universidad -> pais; realizar un llamado entre entidades

> ![](imgs/clase-1/relacion-redundante-2.png)
> 
> En este caso, se quiere consultar en que pais nacio el alumno. Saber en el pais que pertenece la universidad, no es condición necesaria para que alumno sea del mismo (puede ser extranjero). Por lo que es valido crear una relación.

# Clase 2 - Practica DER

---

# Clase 3

---

# Clase 4

---

# Clase 5

---

# Clase 6

---

# Clase 7

---

# Clase 8

---

# Clase 9

---

# Clase 10

---

# Clase 11