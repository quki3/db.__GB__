# BASEDEDATOS.__GB__

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

# Diagrama ER: Platziblog
```bash

              
ENTIDADES{                                    
            usuarios->ATRIBUTOS->{login         posts->ATRIBUTOS->{titulo,          comentarios  categorias  Etiquetas
                                  password      fecha_publicacion,
                                  apodo         contenido,
                                  email         estatus
                                  id}           etiquetas
                                                id}    
          }
            usuarios[1]-[escribe]-[N]comentarios
            usuarios[1]-[escribe]-[N]posts[1]-[tiene]-[N]comentarios
                                     posts[1]-[tiene]-[N]categorias
                                     posts[N]-[tiene]-[N]etiquetas
```
# Diagrama fisico
## tipos de datos
```bash
| TEXTO     | NUMEROS               | FECHA/HORA|LOGOS      |
| :----     | :-------              | :----     |:----      |
| `char(n)` | `interger`            | `date`    |`boolean`  |
| `varcha()`| `bigint  `            | `time`    |
| `text   ` | `smallint`            | `datetime`|
|           | `decimal(n,s)`        | `timestamp`|
|           | `numeric(n,s)`        | 

| Constraint     | Description                                                      | 
| :----          | :-------                                                         | 
|  not null      | se asegura que la columna no tenga valores nulos                 | 
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
