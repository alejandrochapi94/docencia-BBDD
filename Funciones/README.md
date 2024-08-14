Una función es un conjunto de sentencias que operan como una unidad lógica.

Una función tiene un nombre, retorna un parámetro de salida y opcionalmente acepta parámetros de entrada. Las funciones de SQL Server no pueden ser modificadas, las funciones definidas por el usuario si.

SQL Server ofrece varios tipos de funciones para realizar distintas operaciones. Se pueden clasificar de la siguiente manera:

\1) de agregado: realizan operaciones que combinan varios valores y retornan un único valor. Son "count", "sum", "min" y "max".

\2) escalares: toman un solo valor y retornan un único valor. Pueden agruparse de la siguiente manera:

- de configuración: retornan información referida a la configuración.
Ejemplo:

```
 select @@version;
```

retorna la fecha, versión y tipo de procesador de SQL Server.

- de cursores: retornan información sobre el estado de un cursor.

- de fecha y hora: operan con valores "datetime" y "smalldatetime". Reciben un parámetro de tipo fecha y hora y retornan un valor de cadena, numérico o de fecha y hora.

- matemáticas: realizan operaciones numéricas, geométricas y trigonométricas.

\- de metadatos: informan sobre las bases de datos y los objetos.

\- de seguridad: devuelven información referente a usuarios y funciones.

\- de cadena: operan con valores "char", "varchar", "nchar", "nvarchar", "binary" y "varbinary" y devuelven un valor de cadena o numérico.

\- del sistema: informan sobre opciones, objetos y configuraciones del sistema. Ejemplo:

```
 select user_name();
```

\- estadísticas del sistema: retornan información referente al rendimiento del sistema.

\- texto e imagen: realizan operaciones con valor de entrada de tipo text o image y retornan información referente al mismo.

\3) de conjuntos de filas: retornan conjuntos de registros.

Se pueden emplear las funciones del sistema en cualquier lugar en el que se permita una expresión en una sentencia "select".

Estudiaremos algunas de ellas.

## Funciones para manejo de cadenas

Microsoft SQL Server tiene algunas funciones para trabajar con cadenas de caracteres. Estas son algunas:

\- **substring**(cadena,inicio,longitud): devuelve una parte de la cadena especificada como primer argumento, empezando desde la posición especificada por el segundo argumento y de tantos caracteres de longitud como indica el tercer argumento. Ejemplo:

```
 select substring('Buenas tardes',8,6);
```

retorna "tardes".

\- **str**(numero,longitud,cantidaddecimales): convierte números a caracteres; el primer parámetro indica el valor numérico a convertir, el segundo la longitud del resultado (debe ser mayor o igual a la parte entera del número más el signo si lo tuviese) y el tercero, la cantidad de decimales. El segundo y tercer argumento son opcionales y deben ser positivos. String significa cadena en inglés.

Ejemplo: se convierte el valor numérico "123.456" a cadena, especificando 7 de longitud y 3 decimales:

```
 select str(123.456,7,3);

 select str(-123.456,7,3);
```

retorna '-123.46';

Si no se colocan el segundo y tercer argumeno, la longitud predeterminada es 10 y la cantidad de decimales 0 y se redondea a entero. Ejemplo: se convierte el valor numérico "123.456" a cadena:

```
 select str(123.456);
```

retorna '123';

```
 select str(123.456,3);
```

retorna '123';

Si el segundo parámetro es menor a la parte entera del número, devuelve asteriscos (*). Ejemplo: select str(123.456,2,3);

retorna "**".

\- **stuff**(cadena1,inicio,cantidad,cadena2): inserta la cadena enviada como cuarto argumento, en la posición indicada en el segundo argumento, reemplazando la cantidad de caracteres indicada por el tercer argumento en la cadena que es primer parámetro. Stuff significa rellenar en inglés. Ejemplo:

```
 select stuff('abcde',3,2,'opqrs');
```

retorna "abopqrse". Es decir, coloca en la posición 2 la cadena "opqrs" y reemplaza 2 caracteres de la primer cadena.

Los argumentos numéricos deben ser positivos y menor o igual a la longitud de la primera cadena, caso contrario, retorna "null".

Si el tercer argumento es mayor que la primera cadena, se elimina hasta el primer carácter.

\- **len**(cadena): retorna la longitud de la cadena enviada como argumento. "len" viene de length, que significa longitud en inglés. Ejemplo:

```
 select len('Hola');
```

devuelve 4.

\- **char**(x): retorna un caracter en código ASCII del entero enviado como argumento. Ejemplo:

```
 select char(65);
```

retorna "A".

\- **left**(cadena,longitud): retorna la cantidad (longitud) de caracteres de la cadena comenzando desde la izquierda, primer caracter. Ejemplo:

```
 select left('buenos dias',8);
```

retorna "buenos d".

\- **right**(cadena,longitud): retorna la cantidad (longitud) de caracteres de la cadena comenzando desde la derecha, último caracter. Ejemplo:

```
 select right('buenos dias',8);
```

retorna "nos dias".

-**lower**(cadena): retornan la cadena con todos los caracteres en minúsculas. lower significa reducir en inglés. Ejemplo:

```
 select lower('HOLA ESTUDIAnte');
```

retorna "hola estudiante".

-**upper**(cadena): retornan la cadena con todos los caracteres en mayúsculas. Ejemplo:

```
 select upper('HOLA ESTUDIAnte');
```

-**ltrim**(cadena): retorna la cadena con los espacios de la izquierda eliminados. Trim significa recortar. Ejemplo:

```
 select ltrim('     Hola     ');
```

retorna "Hola ".

\- **rtrim**(cadena): retorna la cadena con los espacios de la derecha eliminados. Ejemplo:

```
 select rtrim('   Hola   ');
```

retorna " Hola".

\- **replace**(cadena,cadenareemplazo,cadenareemplazar): retorna la cadena con todas las ocurrencias de la subcadena reemplazo por la subcadena a reemplazar. Ejemplo:

```
 select replace('xxx.sqlserverya.com','x','w');
```

retorna "www.sqlserverya.com'.

\- **reverse**(cadena): devuelve la cadena invirtiendo el order de los caracteres. Ejemplo:

```
 select reverse('Hola');
```

retorna "aloH".

\- **patindex**(patron,cadena): devuelve la posición de comienzo (de la primera ocurrencia) del patrón especificado en la cadena enviada como segundo argumento. Si no la encuentra retorna 0. Ejemplos:

```
 select patindex('%Luis%', 'Jorge Luis Borges');
```

retorna 7.

```
 select patindex('%or%', 'Jorge Luis Borges');
```

retorna 2.

```
 select patindex('%ar%', 'Jorge Luis Borges');
```

retorna 0.

\- **charindex**(subcadena,cadena,inicio): devuelve la posición donde comienza la subcadena en la cadena, comenzando la búsqueda desde la posición indicada por "inicio". Si el tercer argumento no se coloca, la búsqueda se inicia desde 0. Si no la encuentra, retorna 0. Ejemplos:

```
 select charindex('or','Jorge Luis Borges',5); 
```

retorna 13.

```
 select charindex('or','Jorge Luis Borges'); 
```

retorna 2.

```
 select charindex('or','Jorge Luis Borges',14); 
```

retorna 0.

```
 select charindex('or', 'Jorge Luis Borges');
```

retorna 0.

\- **replicate**(cadena,cantidad): repite una cadena la cantidad de veces especificada. Ejemplo:

```
 select replicate ('Hola',3);
```

retorna "HolaHolaHola";

\- **space**(cantidad): retorna una cadena de espacios de longitud indicada por "cantidad", que debe ser un valor positivo. Ejemplo:

```
 select 'Hola'+space(1)+'que tal';
```

retorna "Hola que tal".

Se pueden emplear estas funciones enviando como argumento el nombre de un campo de tipo caracter.

## Resumen funciones para manejo de cadenas

```sql
--Resumen
--substring(cadena,inicio,longitud);
select substring('Holamundo',2,6) as CortarCadena; 

--str(numero,longitud,cadenadedecimales);
select str(123.456,7,3); --toma 7 y 3 decimales
select str(-123.456,7,3); --toma 7 y 2 decimales
select str(123.45); -- toma 3, entero
select str(123.456,3); --toma 3, entero
select str(123.456,5,1); --toma 5, un decimal (redondea)
select str(12.34,4,1); --toma 4, 1 decimal (redondea)
select str(12.35,4,1); --5 o mayor aproxima al siguiente
select str(12.01,4,2); --toma 4, 1 decimal (es lo que alcanza)
select str(123.456,2,1) as asteriscos; -- parte entera mayor a 2 asteriscos

--FUNCIÓN QUE REEMPLAZA TEXTO
--stuff(cadena1,inicio,cantidad,cadena2);
select stuff('hola!Mundo',3,2,'AquiEntroYo'); --quita 2 letras, y reemplaza esta cadena en la posición 3
select stuff('hola',8,6,'mundo'); --ejemplo de un error

--LONGITUD DE UNA CADENA
--len(cadena)retorna un valor numérico

select len('Hola!Gente que tal');
select len(''); --retorna 0

--RETORNO DE VALORES ASCII
select char(65); --retorna A
select char(80); --retorna P

--CORTADOR DE CADENAS A IZQUIERDA Y DERECHA
--left(cadena,longitud);
select left('buenos dias',4);
--right(cadena,longitud);
select right('buenos dias',3);

--CADENAS A MAYUS Y MINUS
--lower(cadena);
--upper(cadena);

--ELIMINAR ESPACIOS A IZQUIERDA Y DERECHA
--ltrim(cadenaConEspaciosAIzquierda);
--rtrim(cadenaConEspaciosADerecha);
select ltrim('   hola');
select rtrim('hola    ');

--REEMPLAZO DE TODAS LAS OCURRENCIAS EN UNA CADENA
--replace(cadena,cadenareemplazo,cadenareemplazar);
select replace('xxx.server.com','x','w');

--HALLAR POSICIÓN DE UN CARACTER EN UNA CADENA DE TEXTO
--patindex(patron,cadena);
select patindex('%Luis%','Jorge Luis Borges');
select patindex('%or%','Jorge Luis Borges');
select patindex('%hola%','Jorge Luis Borges'); --no se encuentra 0

--HALLAR POSICIÓN DE UN CARACTER CON UNA POSICIÓN INICIAL
--charindex(subcadena,cadena,inicio);
select charindex('or','Jorge Luis Borges',5);
select charindex('or','Jorge Luis Borges');
select charindex('or','Jorge Luis Borges',14); --pasado los 14 no hay ninguno retorna 0

--REPETIR UNA CADENA UNA CANTIDAD DE VECES
--replicate(Cadena,cantidad);
select replicate('hola gente',3);

--INGRESAR ESPACIOS EN UNA CADENA
--space(cantidad);
select 'hola'+space(1)+'que tal';
```



### Servidor de SQL Server instalado en forma local.

Ingresemos el siguiente lote de comandos en el SQL Server Management Studio:

```sql
if object_id ('libros') is not null
  drop table libros;

create table libros(
  codigo int identity,
  titulo varchar(40) not null,
  autor varchar(20) default 'Desconocido',
  editorial varchar(20),
  precio decimal(6,2),
  cantidad tinyint default 0,
  primary key (codigo)
);

go

insert into libros (titulo,autor,editorial,precio)
  values('El aleph','Borges','Emece',25);
insert into libros
  values('Java en 10 minutos','Mario Molina','Siglo XXI',50.40,100);
insert into libros (titulo,autor,editorial,precio,cantidad)
  values('Alicia en el pais de las maravillas','Lewis Carroll','Emece',15,50);

-- Mostramos sólo los 12 primeros caracteres de los títulos de los libros y
-- sus autores, empleando la función "substring()":
select substring(titulo,1,12) as titulo
  from libros;

-- Mostramos sólo los 12 primeros caracteres de los títulos de los libros y
-- sus autores, ahora empleando la función "left()":
select left(titulo,12) as titulo
  from libros;

-- Mostramos los títulos de los libros y sus precios convirtiendo este último a cadena
-- de caracteres con un solo decimal, empleando la función "str":
select titulo,
  str(precio,6,1)
  from libros;

-- Mostramos los títulos de los libros y sus precios convirtiendo este último a cadena
-- de caracteres especificando un solo argumento:
select titulo,
  str(precio)
  from libros;

-- Mostramos los títulos, autores y editoriales de todos libros, al último
-- campo lo queremos en mayúsculas:
select titulo, autor, upper(editorial)
   from libros;
```

## Funciones matemáticas

Las funciones matemáticas realizan operaciones con expresiones numéricas y retornan un resultado, operan con tipos de datos numéricos.

Microsoft SQL Server tiene algunas funciones para trabajar con números. Aquí presentamos algunas.

-**abs**(x): retorna el valor absoluto del argumento "x". Ejemplo:

```
 select abs(-20);
```

retorna 20.

-**ceiling**(x): redondea hacia arriba el argumento "x". Ejemplo:

```
 select ceiling(12.34);
```

retorna 13.

-**floor**(x): redondea hacia abajo el argumento "x". Ejemplo:

```
 select floor(12.34);
```

retorna 12.

\- %: %: devuelve el resto de una división. Ejemplos:

```
 select 10%3;
```

retorna 1.

```
 select 10%2;
```

retorna 0.

-**power**(x,y): retorna el valor de "x" elevado a la "y" potencia. Ejemplo:

```
 select power(2,3);
```

retorna 8.

-**round**(numero,longitud): retorna un número redondeado a la longitud especificada. "longitud" debe ser tinyint, smallint o int. Si "longitud" es positivo, el número de decimales es redondeado según "longitud"; si es negativo, el número es redondeado desde la parte entera según el valor de "longitud". Ejemplos:

```
 select round(123.456,1);
```

retorna "123.400", es decir, redondea desde el primer decimal.

```
 select round(123.456,2);
```

retorna "123.460", es decir, redondea desde el segundo decimal.

```
 select round(123.456,-1);
```

retorna "120.000", es decir, redondea desde el primer valor entero (hacia la izquierda).

```
 select round(123.456,-2);
```

retorna "100.000", es decir, redondea desde el segundo valor entero (hacia la izquierda).

-**sign**(x): si el argumento es un valor positivo devuelve 1;-1 si es negativo y si es 0, 0.

-**square**(x): retorna el cuadrado del argumento. Ejemplo:

```
 select square(3); retorna 9.
```

-**srqt**(x): devuelve la raiz cuadrada del valor enviado como argumento.

SQL Server dispone de funciones trigonométricas que retornan radianes.

Se pueden emplear estas funciones enviando como argumento el nombre de un campo de tipo numérico.

```sql
--Resumen Funciones matemáticas
--VALOR ABSOLUTO DE UN NÚMERO
select abs(-20);

--RENDONDEO HACIA ARRIBA Y HACIA ABAJO
--ceiling(x);
--floor(x);
select ceiling(12.3);
select ceiling(12.6);
select floor(12.3);
select floor(12.6);

--MÓDULO O RESTO DE LA DIVISIÓN
--%
select 10%3;

--POTENCIACIÓN
--power(basse,exponente);
select power(3,2);

--REDONDEAR A LA LONGITUD ESPECIFICADA
--round(numero,longitud);
select round(123.456,1);--5 eleva la siguiente cifra
select round(123.446,1);--4 no eleva la siguiente cifra
select round(123.456,2);--6 eleva la siguiente cifra
select round(123.452,2);--2 no eleva la siguiente cifra
select round(123.456,-1);--redondea desde la parte entera (3 hacia abajo)
select round(125.456,-1) as RedondeoHaciaArriba;--redondea la parte entera (5 hacia arriba)
select round(123.456,-2);--redondea la parte entera (2 hacia abajo)
select round(185.456,-2);--redondea la parte entera (8 hacia arriba)

--DEVUELVE UN ARGUMENTO (1 PARA +) (-1 PARA -) (0 PARA 0)
--sign(numero);
select sign(-12);
select sign(12);
select sign(0);

--NÚMERO ELEVADO AL CUADRADO
--square(numero);
select square(9);
select square(10);

--RAIZ CUADRADA
--srqt(numero);
select sqrt(9);--devuelve un entero
select sqrt(10);--devuelve un float
```



### Servidor de SQL Server instalado en forma local.

Ingresemos el siguiente lote de comandos en el SQL Server Management Studio:

```sql
if object_id ('libros') is not null
  drop table libros;

create table libros(
  codigo int identity,
  titulo varchar(40) not null,
  autor varchar(20) default 'Desconocido',
  editorial varchar(20),
  precio decimal(6,2),
  primary key (codigo)
);

go

insert into libros (titulo,autor,editorial,precio)
  values('El aleph','Borges','Emece',25.33);
insert into libros
  values('Java en 10 minutos','Mario Molina','Siglo XXI',50.65);
insert into libros (titulo,autor,editorial,precio)
  values('Alicia en el pais de las maravillas','Lewis Carroll','Emece',19.95);

-- Vamos a mostrar los precios de los libros redondeando el valor hacia abajo y hacia arriba:
select titulo,autor,precio,
  floor(precio) as abajo,
  ceiling(precio) as arriba
  from libros;
```

## FUNCIONES PARA MANEJO DE FECHAS

Microsoft SQL Server ofrece algunas funciones para trabajar con fechas y horas. Estas son algunas:

\- **getdate**(): retorna la fecha y hora actuales. Ejemplo:

```
 select getdate();
```

\- **datepart**(partedefecha,fecha): retorna la parte específica de una fecha, el año, trimestre, día, hora, etc.

Los valores para "partedefecha" pueden ser: year (año), quarter (cuarto), month (mes), day (dia), week (semana), hour (hora), minute (minuto), second (segundo) y millisecond (milisegundo). Ejemplos:

```
 select datepart(month,getdate());
```

retorna el número de mes actual;

```
 select datepart(day,getdate());
```

retorna el día actual;

```
 select datepart(hour,getdate());
```

retorna la hora actual;

\- **datename**(partedefecha,fecha): retorna el nombre de una parte específica de una fecha. Los valores para "partedefecha" pueden ser los mismos que se explicaron anteriormente. Ejemplos:

```
 select datename(month,getdate());
```

retorna el nombre del mes actual;

```
 select datename(day,getdate());
```

\- **dateadd**(partedelafecha,numero,fecha): agrega un intervalo a la fecha especificada, es decir, retorna una fecha adicionando a la fecha enviada como tercer argumento, el intervalo de tiempo indicado por el primer parámetro, tantas veces como lo indica el segundo parámetro. Los valores para el primer argumento pueden ser: year (año), quarter (cuarto), month (mes), day (dia), week (semana), hour (hora), minute (minuto), second (segundo) y millisecond (milisegundo). Ejemplos:

```
 select dateadd(day,3,'1980/11/02');
```

retorna "1980/11/05", agrega 3 días.

```
 select dateadd(month,3,'1980/11/02');
```

retorna "1981/02/02", agrega 3 meses.

```
 select dateadd(hour,2,'1980/11/02');
```

retorna "1980/02/02 2:00:00", agrega 2 horas.

```
 select dateadd(minute,16,'1980/11/02');
```

retorna "1980/02/02 00:16:00", agrega 16 minutos.

\- **datediff**(partedelafecha,fecha1,fecha2): calcula el intervalo de tiempo (según el primer argumento) entre las 2 fechas. El resultado es un valor entero que corresponde a fecha2-fecha1. Los valores de "partedelafecha) pueden ser los mismos que se especificaron anteriormente. Ejemplos:

```
 select datediff (day,'2005/10/28','2006/10/28');
```

retorna 365 (días).

```
 select datediff(month,'2005/10/28','2006/11/29');
```

retorna 13 (meses).

\- **day**(fecha): retorna el día de la fecha especificada. Ejemplo:

```
 select day(getdate());
```

\- **month**(fecha): retorna el mes de la fecha especificada. Ejemplo:

```
 select month(getdate());
```

\- **year**(fecha): retorna el año de la fecha especificada. Ejemplo:

```
 select year(getdate());
```

Se pueden emplear estas funciones enviando como argumento el nombre de un campo de tipo datetime o smalldatetime.

```sql
--Resumen de fechas
--RETORNAR HORA Y FECHA ACTUALES
--getdate();
select getdate();

--OBTENER UN DATO ESPECÍFICO (AÑO,TRIMESTRE,DIA,HORA,ETC)
--datepart(parteDeFecha,fecha);
--OBTENER MES
select datepart(month,getdate());
--OBTENER DIA ACTUAL
select datepart(day,getdate());
--OBTENER HORA ACTUAL
select datepart(hour,getdate());
--TRIMESTRE
select datepart(quarter,getdate());

--OBTENER EL NOMBRE ESPECÍFICO DE UNA FECHA
--datename(partedefecha,fecha);
--OBTENER EL NOMBRE DEL MES
select datename(month,getdate());
--OBTENER EL NOMBRE DEL DÍA
select datename(day,getdate());
--OBTENER EL NOMBRE DEL TRIMESTRE
select datename(quarter,getdate());
--OBTENER EL NOMBRE DE LA HORA
select datename(hour,getdate());

--AGREGAR UN VALOR A UNA FECHA DECLARADA
--retorna "1980/11/05", agrega 3 días.
select dateadd(day,3,'1980/11/02');
--retorna "1981/02/02", agrega 3 meses.
Select dateadd(month,3,'1980/11/02');
--retorna "1980/02/02 2:00:00", agrega 2 horas.
select dateadd(hour,2,'1980/11/02');
--retorna "1980/02/02 00:16:00", agrega 16 minutos.
select dateadd(minute,16,'1980/11/02');

--CALCULAR EL INTERVALO DE TIEMPO ENTRE DOS FECHAS
--datediff(parteDeLaFecha,fecha1,fecha2);
select datediff(day,'2005/10/28','2006/10/28');
 select datediff(month,'2005/10/28','2006/11/29') as mesesDiff;

--RETORNA EL DÍA, MES Y AÑO DE LA FECHA ESPECIFICADA
--day(fecha);
--month(fecha);
--year(fecha);
select day(getdate());
select month(getdate());
select year(getdate());
```

### Servidor de SQL Server instalado en forma local.

Ingresemos el siguiente lote de comandos en el SQL Server Management Studio:

```sql
if object_id ('libros') is not null
  drop table libros;

create table libros(
  titulo varchar(40) not null,
  autor varchar(20) default 'Desconocido',
  editorial varchar(20),
  edicion datetime,
  precio decimal(6,2)
);

go

set dateformat ymd;

insert into libros 
  values('El aleph','Borges','Emece','1980/10/10',25.33);
insert into libros 
  values('Java en 10 minutos','Mario Molina','Siglo XXI','2000/05/05',50.65);
insert into libros 
values('Alicia en el pais de las maravillas','Lewis Carroll','Emece','2000/08/09',19.95);
insert into libros 
  values('Aprenda PHP','Mario Molina','Siglo XXI','2000/02/04',45);

-- Mostramos el título del libro y el año de edición:
select titulo, datepart (year,edicion) from libros;

-- Mostramos el título del libro y el nombre del mes de edición:
select titulo, datename (month,edicion) from libros;

-- Mostramos el título del libro y los años que tienen de editados:
select titulo, datediff(year,edicion,getdate()) from libros;

-- Muestre los títulos de los libros que se editaron el día 9, de cualquier mes de cualquier año:
 select titulo from libros
  where datepart(day,edicion)=9;
```

## Ejercicios de práctica Uso de funciones de echas y hora

```sql
if object_id ('empleados') is not null
  drop table empleados;

create table empleados(
  nombre varchar(30) not null,
  apellido varchar(20) not null,
  documento char(8),
  fechanacimiento datetime,
  fechaingreso datetime,
  sueldo decimal(6,2),
  primary key(documento)
 );
insert into empleados values('Ana','Acosta','22222222','1970/10/10','1995/05/05',228.50);
 insert into empleados values('Carlos','Caseres','25555555','1978/02/06','1998/05/05',309);
 insert into empleados values('Francisco','Garcia','26666666','1978/10/15','1998/10/02',250.68);
 insert into empleados values('Gabriela','Garcia','30000000','1985/10/25','2000/12/22',300.25);
 insert into empleados values('Luis','Lopez','31111111','1987/02/10','2000/08/21',350.98);


--Muestre nombre y apellido concatenados, con el apellido en letras mayúsculas, el documento 
--precedido por "DNI Nº " y el sueldo precedido por "$ ".
select nombre+space(1)+upper(apellido) as Nombres, stuff(documento,1,0,'DNI Nº ') as Documento, stuff(sueldo,1,0,'$ ') as Sueldo from empleados;

--Muestre el documento y el sueldo redondeado hacia arriba y precedido por "$ ".
select documento as Documento, stuff(ceiling(sueldo),1,0,'$ ') as Sueldo from empleados;

--6- Muestre los nombres y apellidos de los empleados que cumplen años en el mes "october" (3 registros)
select nombre, apellido from empleados
  where datename(month,fechanacimiento)='october';

--7- Muestre los nombres y apellidos de los empleados que ingresaron en un determinado año (2 registros)
select nombre,apellido from empleados
  where year(fechaingreso)='1998';
--Otra opción
select nombre,apellido from empleados
  where datepart(year,fechaingreso)=2000;  

```