
# material interesante 
```bash
claves foraneas

https://platzi.com/clases/1566-bd/19810-creando-platziblog-tablas-dependientes/

ingenieria inversa

https://platzi.com/clases/1566-bd/19811-creando-platziblog-tablas-transistivas/
```
# BASE DE DATOS RELACIONALES (RDB)
SQLServer
delfin
elefante
MariaDB
ORACLE
```bash
entidades

manzana
automovil { volante:,
            llantas:,
            motos:,
            pistones:,
            bujias:,
            modelo:,}
laptos{ color:,
        pantalla:,
        nro de serie:}
```



# BASE DE DATOS NO RELACIONALES
cassandra
elasticsearch
neo4j
mongoDB
```bash

```

# servicios
auto administrados
```bash

```
administrados

# Diagrama Fisico
```sql

              
ENTIDADES{                                    
            usuarios->ATRIBUTOS->{
                                    login:VARCHAR(30)NN,                       
                                    password:VARCHAR(32)NN,
                                    niclname:VARCHAR(40)NN,         
                                    email:VARCHAR(40)NN UNIQUE, 
                                    id:INTERGER(PK)
                                  },           
                                                    
           posts->ATRIBUTOS->{      
                                    titulo:VARCHAR(150),
                                    fecha_publicacion:TIMESTAMP,
                                    contenido:TEXT,
                                    estatus:CHAR(8)CHECK(IN('activo,'inactivo'),//esto check si esta activo o inactivo else error
                                    id:INTEGER(PK),
                                    
                                    /*para relacionar las tablas tenemos las claves foraneas es decir se an:ade la clave unica de                                            usuario como clave foranea que hace referencia al user que la creo*/
                                    usuario_id:INTERGER FK
                                    categorias_id:INTERGER FK,
                              },
           comentarios->ATRIBUTOS->{
                                    Id:INTERGER(PK),
                                    comentario:TEXT
                                    
                                    /*para relacionar las tablas tenemos las claves foraneas es decir se an:ade la clave unica de                                            usuario como clave foranea*/
                                    usuario_id:INTERGER FK
                                    posts_id:INTERGER FK
                                    },
           categorias->ATRIBUTOS->{
                                    Id:INTERGER(PK),
                                    categoria:VARCHAR(30)
                                    },
           Etiquetas->{
                                    Id:INTERGER(PK),
                                    nombre_de_etiqueta:VARCHAR(30)
                                    },
           Posts_etiquetas->{
                                    posts_id:INTERGER (PK,FK)
                                    etiquetas_id:INTERGER(PK,FK)
                                    }
          }
          /*REGLAS DE LAS CLAVES FORANEAS
          cuando es de 1-1 no importa a cual le pones la referencia de la otra tabla
          cuando tienes 1-N en la tabla que tiene muchos (N) debes poner la clave foranea
          cuando es de N-N es un caso ESPPECIAL bueno primero tenemos que romper esa relacion N-N poniendo una tabla intermedia
          llamada tabla PIBOTE que nos ayuda a ver cual es la relacion entre ambas entidades, esta tabla por convencion lleva el 
          nombre de ambas entidades/tablas dentro de esta tabla se colocan las dos llaves/id */
```
##  diagrama ER 
```sql
          
            usuarios[1]-[escribe]-[N]comentarios
            usuarios[1]-[escribe]-[N]posts[1]-[tiene]-[N]comentarios
                                     posts[1]-[tiene]-[N]categorias
                                     posts[N]-[tiene]-[N]etiquetas
```
# RDBMS(relational database management system) || Diagrama fisico en forma practica
```sql

```
# CODIGO
## como es el codico en consola para crear entidades con sus atributos
```PosgresSQL
CREATE TABLE ciudades
(
       id serial PRIMARY KEY,
       nombre varchar(255) UNIQUE
 );
CREATE TABLE persona
(
       id serial PRIMARY KEY,
       apellido varchar(255) NOT NULL,
       nombre varchar(255) UNIQUE,
       ciudad interger,
       FORING KEY(ciudad) REFERENCES ciudad(id)//
);
```
## Para insertar entidades, atributos
```sql
INSERT INTO ciudad (nombre) VALUES('tucuman');
INSERT INTO ciudad (nombre) VALUES('Buenos Aires'),('New Yourk'),('Caracas'),('Santa Cruz');
INSERT INTO persona (nombre,apellido,ciudad) VALUES ('toni', 'tralice',1)
```
## Para selecionar  todas las columnas
```sql
select * from ciudad;
select * from persona;
```
## Para selecionar  una columna en especial
```sql
select nombre from ciudad;
select apellido from persona;
select nombre,apellido from persona;

select nombre from persona order by nombre

select * from persona where nombre ='toni'
select * from persona where nombre ='toni' and ciudad =5;
select * from persona where apellidos not in('tralice','tita');
select * from persona where apellidos in('tralice','tita');
select * from persona where id in BETWEEN 4 and 6;

select * from persona where apallido LIKE '%oni%' //? busca una palabra que contenga oni
select * from persona where apallido LIKE 'oni%' //? busca una palabra que empiese con oni
select * from persona where apallido LIKE '%oni' //? busca una palabra que termine con oni
select * from persona where apallido ILIKE '%oni' //? busca una palabra que termine con oni ILIKE evita tener problemas de mayusculas 

select distinct nombre from persona

select (nombre || " " apellido) as "Nombre y Apellido" from persona // concatena esas busquedas como string
select concat(nombre,' ', apellido) from persona; //  concatena esas busquedas como string
select * from persona where ciudad in (select id from ciudad where nombre='Tucuman');//?selecciona todo de persona donde la ciudad tiene nombre tucuman treme el id

select COUNT(*) from persona; //? cuenta las personas 
select ciudad, COUNT(ciudad) from persona GROUP BY ciudad;//?cuenta las personas de cada ciudad
select ciudad, nombre, count(ciudad) from persona group by ciudad, nombre;//? esto cuenta las ciudades y empareja las que tengan el mismo nombre y ciudad
select ciudad, nombre, count(ciudad) from persona group by ciudad, nombre having count(ciudad) > 1;//?


```
# Diagrama fisico
## tipos de datos
```bash
| TEXTO     |               | 
| :----     | :-------              |
| `char(size)` | `size decribe el numero de caracteres a guardar`            | 
| `varcha()`| `permite tener una longitud variable `            | 
| `text ` | `la longitud es variable no me importa el valor el size`            | 

| NUMEROS               |           |
| :-------              | :----     |
| `interger`            | `equivale a 4bytes`    |
| `bigint  `            | `equivale a 8 bytes`  |
| `smallint`            | `equivale a 2bytes`|
| `decimal(n,s)`        | `timestamp`|
| `numeric(n,s)`        | si trabajamos con numeros decimales |
| `serial`              | se autoincrementa |
| `double precision` | `doble presicion 8 bytes`|
|`real`                 |presicion simple 4 bytes|

| FECHA/HORA|      |
| :----     |:----      |
| `date`    |`yyyy-mm-dd`  |
|`time`     |hh:mm:ss|
| `timestamp`|yyyy-mm-dd hh:mm:ss|
| `timestamp without time zone`|yyyy-mm-dd hh:mm:ss-tz|
| `datetime`|
| `timestamp`|
| 


| Constraint     | Description                                                      | 
| :----          | :-------                                                         | 
|  not null (NN)     | se asegura que la columna no tenga valores nulos                 | 
|  unique        | se asegura que cada valor en la columna no se repita             | 
|  primary key   | es una combinacion de not null  y unique                         | 
|  foreing key   | identifica de manera unica una tupla en otra tabla               | 
|  check         | se asegura que el valor en la columna cumpla una condicion dada  | 
|  default       | coloca un valor por defecto cuando no hay un valor especificado  | 
|  index         | se crea por columna para pernitir busquedas mas rapidas          | 
```
char->statico guarda un espacio fijo de memoria
varchar->dinamico va a cambiar dependiendo de el tamanio de dato
text->para guardar datos grandos mas 500caracteres
# Relaciones y cardinalidad
```bash
            Automovil---(relacion)[__TIENE__]---Duen:o
            
            Jugadores---(relacion)[__PERTENECE__]---equipo
            
     cardinalidad 1-1
     una persona solo puede tener una serie de datos personales y los datos personales 
     solo pueden pertenecer a una persona
            persona-[1]---(relacion)[__TIENE__]---[1]-datos_contacto
     
     cardinalidad 0-1
     la sesion actual tiene que tener un usuario pero el usuario puede que no este en una sesion actual
            sesion_actual-[0]---(relacion)[__TIENE__]---[1]-usuario
     
     cardinalidad 1-N
     una persona puede tener muchos autos pero un auto pertenese solo a una persona
            persona-[1]---(relacion)[__TIENE__]---[N]-automovil
     cardinalidad 0-N
     un pasiente tiene que tener una habitacion de hospital pero una habitacion de hospital puede que no tenga 
     pasientes
            paciente-[0]---(relacion)[__TIENE__]---[N]-habitacion_hospital
     cardinalidad N-N
     un alumno puede tomar varias clases y una clase contiene varios alumnos
            alumno-[N]---(relacion)[__PERTENECE__]---[N]-clase
```
# Normalizacion
```bash
SIN NORMALIZAR
|ALUMNOS|
| ALUMNOS   | NIVEL DE CURSO        | NOMBRE DE CURSO       |MATERIA 1              |MATERIA 2              |
| :----     | :-------              | :----                 |:----                  |:----                  |
| juanito   |maestria               | data engineering      |MySQL                  |Python                 |
| pepito    | licenciatura          | programacion          |MsSQL                  |Python                 |

PRIMERA FORMA NORMAL(1FN)
Atributos atomicos (sin campos repetidos)
|alumno id  | ALUMNO   | NIVEL DE CURSO        | NOMBRE DE CURSO       |MATERIA               |
| :----     | :----     | :-------              | :----                 |:----                  |
|1          | juanito   |maestria               | data engineering      |MySQL                  |
|1          | juanito   | maestria              | data engineering     |Python                  |
|2          | pepito    |licenciatura           | programacion        |MySQL                  |
|2          | pepito    | licenciatura          | programacion         |Python                 |

SEGUNDA FORMA NORMAL(2FN)
Cumple 1FN y cada campo de la tabla debe depender de una clave unica
|alumnos|
|alumno id  | ALUMNO   | NIVEL DE CURSO        | NOMBRE DE CURSO       |
| :----     | :----     | :-------              | :----                 |
|1          | juanito   |maestria               | data engineering      |
|2          | pepito    |licenciatura           | programacion        |

|materias|
|materia id  | ALUMNO id| materia   |
| :----     | :----     | :------   | 
|1          |1          |MySQL      |
|2          |1          |Python     |
|3          |2          |MySQL      |
|4          |2          |Python     |

TERCERA FORMA NORMAL (3FN)
Cumple 1FN y 2FN y los campos que no son clave no deben tener dependencias
|alumnos|
|alumno id  | ALUMNO    |curso id   |
| :----     | :----     | :------   |
|1          |juanito    |1          |
|2          |pepito     |2          |

|cursos|
| NIVEL DE CURSO        | NOMBRE DE CURSO       | curso id  |
| :----                 | :----                 | :------   |
|Maestria               |data engieneering      |1          |
|licenciatura           |programacion           |2          |

|materias|
|materia id  | ALUMNO id| materia   |
| :----     | :----     | :------   | 
|1          |1          |MySQL      |
|2          |1          |Python     |
|3          |2          |MySQL      |
|4          |2          |Python     |


CUARTA FORMA NORMAL(4FN)
cumple 1FN,2FN y 3FN los campos multivaluados se identifican por una unica clave

|alumnos|
|alumno id  | ALUMNO    |curso id   |
| :----     | :----     | :------   |
|1          |juanito    |1          |
|2          |pepito     |2          |

|cursos|
| NIVEL DE CURSO        | NOMBRE DE CURSO       | curso id  |
| :----                 | :----                 | :------   |
|Maestria               |data engieneering      |1          |
|licenciatura           |programacion           |2          |

|materias|
|materia id  | ALUMNO id| mpa id   |
| :----     | :----     | :------   | 
|1          |1          |1     |
|2          |1          |2     |
|1          |2          |3      |
|2          |2          |4    |

|materias|
|materia id  | materia|
| :----     | :----     |
|1          |MySQL      |
|2          |Python     |
```
# ORMs (Object-relational-mapping)
interpreta la basededatos y la pasa a obj y biseversa
```bash

```
# Consultas o querys
Estructura basica de un query
```bash
SELECT
FROM
WHERE
----------------
SELECT city, count(*) AS total //?selecciona city como una cuenta y la proyecta como total
FROM people //?tomamos los datos de la tabla people
WHERE active = true //? la condicion que dice traeme solo los que en activer traen la condicion true
GROUP BY city //? agrupa las personas por un criterio en este caso ciudad
ORDER BY total DESC //? ordena por ciudad en decendiente
HAVING total >= 2; //? filtra el total cuando halle mas d edos personas por city
```
