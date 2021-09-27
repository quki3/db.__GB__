# PostSQL 
```bash
\l =>? lista todas las bases de datos creadas
create database sql; =>? crea una base de datos
\c nombredelabasededatos =>? entra a la base de datos
\dt =>?lista todas las tablas
\d =>?lista todas las tablas
\! clear =>? limpia la pantalla
```
## code
```sql
CREATE DATABASE prueba;
USE DATABASE nombredelabasededatos;
CREATE TABLE ciudades
(
  id serial PRIMARY KEY,
  nombre varchar(255) UNIQUE
);

CREATE TABLE personas
(
  id serial PRIMARY KEY,
  apellido varchar(255) NOT NULL,
  nombre varchar(255) UNIQUE,
  ciudad integer references ciudades (id)
);

INSERT INTO ciudades (nombre)
VALUES ('Tucuman');

INSERT INTO ciudades (nombre)
VALUES ('Buenos Aires');

INSERT INTO ciudades (nombre)
VALUES ('New York');

```
## queris
```sql
SELECT
SELECT column_name,column_name FROM table_name;
SELECT * FROM personas;
SELECT * FROM ciudades;

ORDER BY
SELECT * FROM ciudades ORDER BY nombre;
SELECT * FROM ciudades ORDER BY nombre, id DESC;
GROUP BY
SELECT first_name, last_name, count(*) as total FROM actors GROUP BY LOWER(first_name), LOWER(last_name) ORDER BY total DESC LIMIT 10

WHERE
SELECT column_name,column_name FROM table_name WHERE column_name operator value;
SELECT * FROM personas WHERE nombre = 'Toni';
SELECT * FROM personas WHERE nombre = 'Toni' AND apellido = 'Tralice';

JOIN
SELECT * FROM personas JOIN ciudades  ON ciudades.id = personas.ciudad;
SELECT p.nombre, p.apellido, c.nombre FROM personas p JOIN ciudades  c ON c.id = p.ciudad;

COUNT(*)
SELECT COUNT(*) AS total FROM movies WHERE year=algo

```
