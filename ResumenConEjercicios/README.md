# Curso Bases de datos (sql server)

## Creación de una base de datos

```sql
create database db1;
```

Con este comando creamos la primera base de datos.

## Creación de una tabla dentro de la base de datos

- Clic derecho en la base de datos
- New Query

```sql
create table usuarios(
	nombre varchar(30),
	clave varchar(10));
```

## Ver los datos de la tabla

```sql
exec sp_columns usuarios;
```

## Eliminar una tabla dentro de la base de datos

```sql
drop table usuarios;
```

## Creación de una base de datos, una tabla y llenar la tabla.

```sql
if object_id('usuarios') is not null
	drop table usuarios;

create table usuarios(
	nombre varchar(30),
	clave varchar(10)
);

insert into usuarios(nombre, clave) values('Alejandro','TM1234');

select * from usuarios;

insert into usuarios(nombre, clave) 

values('Belén','Agosto123');
select * from usuarios;

```

varchar() -> cadena de caracteres

## Tipos de datos básicos cuando declaramos campos de una tabla

```sql
if object_id('libros') is not null
	drop table libros;

create table libros(
	titulo varchar(40),
	autor varchar(30),
	editorial varchar(30),
	precio float,
	cantidad integer
);
exec sp_columns libros;


insert into libros(titulo, autor, editorial, precio, cantidad) values('libro 1','autor 1','Estrella', 12.50, 200);
select * from libros;

insert into libros(titulo, autor, editorial, precio, cantidad) values('libro 2','autor 2','Estrella 2', 13.50, 300);

insert into libros(titulo, autor, editorial, precio, cantidad) values('libro 3','autor 3','Estrella 3', 14.50, 400);


select * from libros;

```

# Cláusula Where

```sql
if object_id('amigos') is not null
	drop table amigos;

create table amigos(
	nombre varchar(30),
	clave varchar(30)
);

go

exec sp_columns amigos;

insert into amigos(nombre, clave) values('Marcelo','Boca');
insert into amigos(nombre, clave) values('JuanPerez','Juancito');
insert into amigos(nombre, clave) values('Susana','River');
insert into amigos(nombre, clave) values('Luis','River');

--Recuperamos el usuario cuyo nombre es "Leonardo"
select * from amigos
	where nombre='Leonardo';

--Recuperamos el nombre de los usuarios cuya clave es "River"
select * from amigos
	where clave='River';
	
--Recuperamos el nombre de los usuarios cuya clave es "Santi"
select * from amigos
	where clave='Santi';


```

## Ejercicio 1

```sql
--Ejercicio Where (Curso SQL Y)
if object_id('agenda') is not null
	drop table agenda;

create table agenda(
	apellido varchar(30),
	nombre varchar(30),
	domicilio varchar(30),
	telefono varchar(30)
);

exec sp_columns agenda;

insert into agenda(apellido, nombre, domicilio, telefono) values('Acosta','Ana','Colon 123','4234567');
insert into agenda(apellido, nombre, domicilio, telefono) values('Bustamante','Betina','Avellaneda 135','4458787');
insert into agenda(apellido, nombre, domicilio, telefono) values('Lopez','Hector','Salta 545','4887788');
insert into agenda(apellido, nombre, domicilio, telefono) values('Lopez','Luis','Urquiza 333','4545454');
insert into agenda(apellido, nombre, domicilio, telefono) values('Lopez','Marisa','Urquiza 333','4545454');

select * from agenda;

select * from agenda
	where nombre='Marisa';

select * from agenda
	where apellido='Lopez';

select * from agenda
	where telefono='4545454';
```

## Ejercicio 2

```sql
if object_id('libreria') is not null
	drop table libreria;

create table libreria(
	titulo varchar(30),
	autor varchar(30),
	editorial varchar(15)
	);

exec sp_columns libreria;

insert into libreria(titulo, autor, editorial) values('El aleph','Borges','Emece');
insert into libreria(titulo, autor, editorial) values('Martin Fierro','Jose Hernandez','Emece');
insert into libreria(titulo, autor, editorial) values('Martin Fierro','Jose Hernandez','Planeta');
insert into libreria(titulo, autor, editorial) values('Aprenda PHP','Mario Molina','Siglo XXI');

--Seleccionar los registros que tienen el autor "Borges"
select * from libreria
	where autor = 'Borges';
--Seleccionar los títulos de los libros cuya editorial sea "Emece"
select titulo, editorial from libreria
	where editorial = 'Emece';
--Seleccionar las editoriales de los libros cuyo título sea "Martin Fierro"
select editorial, titulo from libreria
	where titulo= 'Martin Fierro';

```

## Operadores Relacionales

SQL Server tiene 4 tipos de operadores:

1. Relacionales (o de comparación)
2. Aritméticos
3. De concatenación
4. Lógicos

Los operadores relacionales (o de comparación) nos permiten comparar dos expresiones, que pueden ser variables, valores de campos, etc.

Los operadores relacionales son los siguientes:

> = igual
> <> distinto
> < mayor
> < menor
> '>=' mayor o igual
> <= menor o igual

#### Ejemplo

```sql
select titulo, precio
	from libros
	where precio > 20;

select * from libros
	where precio>=30;
```

### Ejercicio de aplicación

```sql
if object_id('libros') is not null
  drop table libros;

create table libros(
  titulo varchar(30),
  autor varchar(30),
  editorial varchar(15),
  precio float
);

go

insert into libros (titulo,autor,editorial,precio)
  values ('El aleph','Borges','Emece',24.50);
insert into libros (titulo,autor,editorial,precio)
  values ('Martin Fierro','Jose Hernandez','Emece',16.00);
insert into libros (titulo,autor,editorial,precio)
  values ('Aprenda PHP','Mario Molina','Emece',35.40);
insert into libros (titulo,autor,editorial,precio)
  values ('Cervantes y el quijote','Borges','Paidos',50.90);

-- Seleccionamos los registros cuyo autor sea diferente de 'Borges'
select * from libros
  where autor<>'Borges';

-- Seleccionamos los registros cuyo precio supere los 20 pesos, sólo el título y precio
select titulo,precio
  from libros
  where precio>20;

-- Recuperamos aquellos libros cuyo precio es menor o igual a 30
select * from libros
  where precio<=30;
```

### Ejercicio

```sql
if object_id('articulos') is not null
	drop table articulos;

create table articulos(
	codigo integer,
	nombre varchar(20),
	descripcion varchar(30),
	precio float,
	cantidad integer
	);

exec sp_columns articulos;

insert into articulos (codigo, nombre, descripcion, precio,cantidad)
  values (1,'impresora','Epson Stylus C45',400.80,20);
 insert into articulos (codigo, nombre, descripcion, precio,cantidad)
  values (2,'impresora','Epson Stylus C85',500,30);
 insert into articulos (codigo, nombre, descripcion, precio,cantidad)
  values (3,'monitor','Samsung 14',800,10);
 insert into articulos (codigo, nombre, descripcion, precio,cantidad)
  values (4,'teclado','ingles Biswal',100,50);
 insert into articulos (codigo, nombre, descripcion, precio,cantidad)
  values (5,'teclado','español Biswal',90,50);

select * from articulos
	where nombre='impresora';

select nombre from articulos
	where precio>=400;

select codigo, nombre from articulos
	where cantidad < 30;

select nombre, descripcion from articulos
	where precio <> 100;
```

### Segundo ejercicio

```sql
if object_id('peliculas') is not null
	drop table peliculas;

create table peliculas(
	titulo varchar(20),
	actor varchar(20),
	duracion integer,
	cantidad integer
);

go

insert into peliculas (titulo, actor, duracion, cantidad)
  values ('Mision imposible','Tom Cruise',120,3);
 insert into peliculas (titulo, actor, duracion, cantidad)
  values ('Mision imposible 2','Tom Cruise',180,4);
 insert into peliculas (titulo, actor, duracion, cantidad)
  values ('Mujer bonita','Julia R.',90,1);
 insert into peliculas (titulo, actor, duracion, cantidad)
  values ('Elsa y Fred','China Zorrilla',80,2);

select * from peliculas
	where duracion <= 90;

select titulo from peliculas
	where actor <> 'Tom Cruise';

select titulo, actor,cantidad from peliculas
	where cantidad > 2;

```

## Borrar registros (delete)

Para eliminar registros de una tabla usamos el comando "delete".

```sql
delete from usuarios;
```

Muestra un mensaje indiciando la cantidad de registros que se han eliminado.

Se usa junto a la cláusula where.

```sql
delete from usuarios
	where nombre='Marcelo';
```

Si solicitamos el borrado de un registro que no existe, es decir, ningún registro cumple con la condición especificada, ningún registro será eliminado.

#### Ejemplo

```sql
if object_id('usuarios') is not null
  drop table usuarios;

create table usuarios(
  nombre varchar(30),
  clave varchar(10)
);

go

insert into usuarios (nombre,clave)
  values ('Marcelo','River');
insert into usuarios (nombre,clave)
  values ('Susana','chapita');
insert into usuarios (nombre,clave)
  values ('CarlosFuentes','Boca');
insert into usuarios (nombre,clave)
  values ('FedericoLopez','Boca');

select * from usuarios;

-- Eliminamos el registro cuyo nombre de usuario es "Marcelo"
delete from usuarios
  where nombre='Marcelo';

select * from usuarios;

-- Intentamos eliminarlo nuevamente (no se borra registro)
delete from usuarios
 where nombre='Marcelo';

select * from usuarios;

-- Eliminamos todos los registros cuya clave es 'Boca'
delete from usuarios
  where clave='Boca';

select * from usuarios;

-- Eliminemos todos los registros
delete from usuarios;

select * from usuarios;
```

### Ejercicio 1

```sql
--Agenda con comando delete y where

if object_id('agenda') is not null
	drop table agenda;

create table agenda(
	apellido varchar(30),
	nombre varchar(20),
	domicilio varchar(30),
	telefono varchar(11)
);

go

insert into agenda(apellido,nombre,domicilio,telefono) values('Alvarez','Alberto','Colon 123','4234567');
insert into agenda(apellido,nombre,domicilio,telefono) values('Lopez','Maria','Urquiza 333','4458787');
insert into agenda(apellido,nombre,domicilio,telefono) values('Juarez','Juan','Avellaneda 135','4545454');
insert into agenda(apellido,nombre,domicilio,telefono) values('Lopez','Jose','Urquiza 333','4545454');
insert into agenda(apellido,nombre,domicilio,telefono) values('Salas','Susana','Gral. Paz 1234','4123456');

exec sp_columns agenda;
select * from agenda;

delete from agenda
	where nombre='Juan';

select * from agenda;

delete from agenda
	where telefono='4545454';

select * from agenda;

delete from agenda;

select * from agenda;
```

#### Ejercicio 2

```sql
if object_id('articulos') is not null
	drop table articulos;

create table articulos(
	codigo integer,
    nombre varchar(20),
    descripcion varchar(30),
    precio float,
    cantidad integer
);
go

exec sp_columns articulos;

insert into articulos (codigo, nombre, descripcion, precio,cantidad)
  values (1,'impresora','Epson Stylus C45',400.80,20);
 insert into articulos (codigo, nombre, descripcion, precio,cantidad)
  values (2,'impresora','Epson Stylus C85',500,30);
 insert into articulos (codigo, nombre, descripcion, precio,cantidad)
  values (3,'monitor','Samsung 14',800,10);
 insert into articulos (codigo, nombre, descripcion, precio,cantidad)
  values (4,'teclado','ingles Biswal',100,50);
 insert into articulos (codigo, nombre, descripcion, precio,cantidad)
  values (5,'teclado','español Biswal',90,50);
  
  --
  delete from articulos
  	where precio>=500;
  select * from articulos;
  delete from articulos
  	where nombre='impresora';
  select * from articulos;
  delete from articulos
  	where codigo<>4;
  select * from articulos;
  


```

## Actualizar registros

Para modificar registros utilizamos "update" (actualizar).

Utilizamos "update" junto al nombre de la tabla y "set" junto con el campo a modificar y su nuevo valor. Este cambio afectará a todos los registros.

Podemos modificar algunos registros, para ello debemos establecer condiciones de selección con "where". Por ejemplo:

```sql
update usuarios set clave='Boca'
	where nombre='Federico'
```

También podemos actualizar varios campos de una sola instrucción.

```sql
update usuarios set nombre='MarceloDuarte', clave='Marce'
	where nombre='Marcelo';
```

#### Ejercicio 1

```sql
if object_id('agenda') is not null
	drop table agenda;

create table agenda(
	apellido varchar(30),
	nombre varchar(30),
	domicilio varchar(30),
	telefono varchar(11)
);
go

insert into agenda (apellido,nombre,domicilio,telefono)
  values ('Acosta','Alberto','Colon 123','4234567');
 insert into agenda (apellido,nombre,domicilio,telefono)
  values ('Juarez','Juan','Avellaneda 135','4458787');
 insert into agenda (apellido,nombre,domicilio,telefono)
  values ('Lopez','Maria','Urquiza 333','4545454');
 insert into agenda (apellido,nombre,domicilio,telefono)
  values ('Lopez','Jose','Urquiza 333','4545454');
 insert into agenda (apellido,nombre,domicilio,telefono)
  values ('Suarez','Susana','Gral. Paz 1234','4123456');


exec sp_columns agenda;

select * from agenda;

update agenda set nombre='Juan Jose'
	where nombre = 'Juan';

select * from agenda;

update agenda set telefono = '4445566'
	where telefono = '4545454';

select * from agenda;

update agenda set nombre='Juan Jose'
	where nombre = 'Juan';

select * from agenda;

```

#### Ejercicio 2

```sql
if object_id('libros') is not null
	drop table libros;

create table libros(
	titulo varchar(30),
	autor varchar(20),
	editorial varchar(15),
	precio float
);

go

 insert into libros (titulo, autor, editorial, precio)
  values ('El aleph','Borges','Emece',25.00);
 insert into libros (titulo, autor, editorial, precio)
  values ('Martin Fierro','Jose Hernandez','Planeta',35.50);
 insert into libros (titulo, autor, editorial, precio)
  values ('Aprenda PHP','Mario Molina','Emece',45.50);
 insert into libros (titulo, autor, editorial, precio)
  values ('Cervantes y el quijote','Borges','Emece',25);
 insert into libros (titulo, autor, editorial, precio)
  values ('Matematica estas ahi','Paenza','Siglo XXI',15);




exec sp_columns libros;

select * from libros;

update libros set autor='Adrian Paenza'
	where autor='Paenza';
select * from libros;

update libros set autor='Adrian Paenza'
	where autor='Paenza';
select * from libros;

update libros set precio=27
	where autor='Mario Molina';
select * from libros;

update libros set editorial='Emece S.A.'
	where editorial='Emece';
select * from libros;


```

## Valores not null (is null)

"null" significa dato desconocido o valor inexistente. No es lo mismo que un valor "0", una cadena vacía o una cadena literal "null".

A veces, puede desconocerse o no existir el dato correspondiente a algún campo de un registro. En estos casos decimos que el campo puede contener valores nulos.

Por ejemplo, en nuestra tabla de libros, podemos tener valores nulos en el campo "precio" porque es posible que para algunos libros no le hayamos establecido el precio para la venta.

En contraposición, tenemos campos que no pueden estar vacíos jamás.

Veamos un ejemplo. Tenemos nuestra tabla "libros". El campo "titulo" no debería estar vacío nunca, igualmente el campo "autor". Para ello, al crear la tabla, debemos especificar que dichos campos no admitan valores nulos:

```sql
create table libros(
  titulo varchar(30) not null,
  autor varchar(20) not null,
  editorial varchar(15) null,
  precio float 
 );
```

Para especificar que un campo no admita valores nulos, debemos colocar "not null" luego de la definición del campo.
En el ejemplo anterior, los campos "editorial" y "precio" si admiten valores nulos.
Cuando colocamos "null" estamos diciendo que admite valores nulos (caso del campo "editorial"); por defecto, es decir, si no lo aclaramos, los campos permiten valores nulos (caso del campo "precio").

```sql
insert into libros (titulo,autor,editorial,precio)
  values('El aleph','Borges','Emece',null);
```

Note que el valor "null" no es una cadena de caracteres, no se coloca entre comillas.
Entonces, si un campo acepta valores nulos, podemos ingresar "null" cuando no conocemos el valor.

También podemos colocar "null" en el campo "editorial" si desconocemos el nombre de la editorial a la cual pertenece el libro que vamos a ingresar:

```sql
insert into libros (titulo,autor,editorial,precio)
  values('Alicia en el pais','Lewis Carroll',null,25);
```

Si intentamos ingresar el valor "null" en campos que no admiten valores nulos (como "titulo" o "autor"), SQL Server no lo permite, muestra un mensaje y la inserción no se realiza; por ejemplo:

```sql
 insert into libros (titulo,autor,editorial,precio)
  values(null,'Borges','Siglo XXI',25);
```

Para ver cuáles campos admiten valores nulos y cuáles no, podemos emplear el procedimiento almacenado "sp_columns" junto al nombre de la tabla. Nos muestra mucha información, en la columna "IS_NULLABLE" vemos que muestra "NO" en los campos que no permiten valores nulos y "YES" en los campos que si los permiten.

Para recuperar los registros que contengan el valor "null" en algún campo, no podemos utilizar los operadores relacionales vistos anteriormente: = (igual) y <> (distinto); debemos utilizar los operadores "is null" (es igual a null) y "is not null" (no es null):

```
select * from libros
  where precio is null;
```

La sentencia anterior tendrá una salida diferente a la siguiente:

```sql
select * from libros
  where precio=0;
```

Con la primera sentencia veremos los libros cuyo precio es igual a "null" (desconocido); con la segunda, los libros cuyo precio es 0.

Igualmente para campos de tipo cadena, las siguientes sentencias "select" no retornan los mismos registros:

```sql
select * from libros where editorial is null;
 select * from libros where editorial='';
```

Con la primera sentencia veremos los libros cuya editorial es igual a "null", con la segunda, los libros cuya editorial guarda una cadena vacía.

Entonces, para que un campo no permita valores nulos debemos especificarlo luego de definir el campo, agregando "not null". Por defecto, los campos permiten valores nulos, pero podemos especificarlo igualmente agregando "null".

#### Ejemplo 1

```sql
if object_id('libros') is not null
   drop table libros;

create table libros(
  titulo varchar(30) not null,
  autor varchar(30) not null,
  editorial varchar(15) null,
  precio float
);

go

-- Agregamos un registro a la tabla con valor nulo para el campo "precio":
insert into libros (titulo,autor,editorial,precio)
  values('El aleph','Borges','Emece',null);

-- Ingresamos otro registro, con valor nulo para el campo "editorial"
insert into libros (titulo,autor,editorial,precio)
  values('Alicia en el pais','Lewis Carroll',null,0);

-- Veamos lo que sucede si intentamos ingresar el valor "null"
-- en campos que no lo admiten, como "titulo":
 insert into libros (titulo,autor,editorial,precio)
  values(null,'Borges','Siglo XXI',25);

exec sp_columns libros;

-- Dijimos que el valor "null" no es lo mismo que una cadena vacía. 
-- Vamos a ingresar un registro con cadena vacía para el campo "editorial":
insert into libros (titulo,autor,editorial,precio)
  values('Uno','Richard Bach','',18.50);

-- Ingresamos otro registro, ahora cargamos una cadena vacía en el campo "titulo":
insert into libros (titulo,autor,editorial,precio)
  values('','Richard Bach','Planeta',22);

select * from libros;

-- Recuperemos los registros que contengan el valor "null" en el campo "precio":
select * from libros
  where precio is null;

-- La sentencia anterior tendrá una salida diferente a la siguiente:
select * from libros
  where precio=0;

-- Recuperemos los libros cuyo nombre de editorial es "null":
 select * from libros
  where editorial is null;

-- Ahora veamos los libros cuya editorial almacena una cadena vacía:
 select * from libros
  where editorial=''; 

-- Para recuperar los libros cuyo precio no sea nulo tipeamos:
 select * from libros
  where precio is not null;
```

### Ejercicio 1

```sql
if object_id('medicamentos') is not null
	drop table medicamentos;

create table medicamentos(
	codigo integer not null,
	nombre varchar(20) not null,
	laboratorio varchar(20) not null,
	precio float,
	cantidad integer not null
	);

go

exec sp_columns medicamentos;

--valores que botan error en la ejecución
/* 
insert into medicamentos (codigo,nombre,laboratorio,precio,cantidad)
  values(1,'Sertal gotas',null,null,100); 

 insert into medicamentos (codigo,nombre,laboratorio,precio,cantidad)
  values(2,'Sertal compuesto',null,8.90,150); */
--código correcto
 insert into medicamentos (codigo,nombre,laboratorio,precio,cantidad)
  values(3,'Buscapina','Roche',0,200);

 insert into medicamentos (codigo,nombre,laboratorio,precio,cantidad)
  values(3,'Ayayai','',null,100);


select * from medicamentos;

insert into medicamentos(codigo,nombre,laboratorio,precio,cantidad) values(0,'','LAB1',15.60,0);

select * from medicamentos;

/* código que devuelve un error ya que codigo no acepta null
insert into medicamentos (codigo,nombre,laboratorio,precio,cantidad)
  values(null,'Amoxidal jarabe','Bayer',25,120);

*/

select * from medicamentos
	where laboratorio is null;

select * from medicamentos
	where laboratorio = '';
--precio null y precio igual a 0
select * from medicamentos
	where precio is null;

select * from medicamentos
	where precio = 0;
--laboratorio vacío y no null
select * from medicamentos
	where laboratorio<>'';
select * from medicamentos
	where laboratorio is not null;
--precio diferente de cero y no null
select * from medicamentos
	where precio <> 0;
select * from medicamentos
	where precio is not null;
```

#### Ejercicio 2

```sql
if object_id('peliculas') is not null
	drop table peliculas;

create table peliculas(
	codigo int not null,
  titulo varchar(40) not null,
  actor varchar(20),
  duracion int
);

go

exec sp_columns peliculas;

insert into peliculas (codigo,titulo,actor,duracion)
  values(1,'Mision imposible','Tom Cruise',120);
 insert into peliculas (codigo,titulo,actor,duracion)
  values(2,'Harry Potter y la piedra filosofal',null,180);
 insert into peliculas (codigo,titulo,actor,duracion)
  values(3,'Harry Potter y la camara secreta','Daniel R.',null);
 insert into peliculas (codigo,titulo,actor,duracion)
  values(0,'Mision imposible 2','',150);
 insert into peliculas (codigo,titulo,actor,duracion)
  values(4,'','L. Di Caprio',220);
 insert into peliculas (codigo,titulo,actor,duracion)
  values(5,'Mujer bonita','R. Gere-J. Roberts',0);

select * from peliculas;

/*código que no ejecuta 
insert into peliculas (codigo,titulo,actor,duracion)
  values(null,'Mujer bonita','R. Gere-J. Roberts',190);
*/

select * from peliculas
	where actor is null;

select * from peliculas
	where actor='';

select * from peliculas;

update peliculas set duracion=120
	where duracion is null;

select * from peliculas;

update peliculas set actor = 'Desconocido'
	where actor='';

select * from peliculas;

delete peliculas
	where titulo='';

select * from peliculas;

```