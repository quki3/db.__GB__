# MySQL
## code MySQL
```mysql
DDL
CREATE
CREATE SCHEMA nombredelabasededatos DEFAULT CHARACTER SET utf8
CREATE TABLE 'nombredelabasededatos'.'nombredelatabla'(
  person_id INT NOT NULL AUTO_INCREMENT,
  last_name VARCHAR(255) NULL,
  firt_name VARCHAR(255) NULL,
  address VARCHAR(255) NULL,
  city VARCHAR(255) NULL,
  PRIMARY KEY ('person_id)
);
CREATE OR REPLACE VIEWS 'nombredelaviews' AS SELECT * FROM nombredelabasededatos.nombredelatabla;

USE 'nombredelabasededatos';

Alter
ALTER TABLE 'nombredelabasededatos'.'nombredelatabla' ADD COLUMN 'date_of_birth' DATETIME NULL AFTER 'city';
ALTER TABLE 'nombredelabasededatos'.'nombredelatabla' CHANGE COLUMN 'date_of_birth' 'date_of_birth' VARCHAR(30) NULL DEFAULT NULL;
ALTER TABLE 'nombredelabasededatos'.'nombredelatabla' DROP COLUMN 'date_of_birth';

Drop
DROP TABLE 'nombredelabasededatos'.'nombredelatabla';
DROP DATABASE 'nombredelabasededatos';


DML
INSERT
INSERT INTO nombredetabla (last_name, first_name, address, city) VALUES ('Hernandez', 'Laure','Calle 21', 'Monterrey);

UPDATE
UPDATE nombredetabla SET last_name = 'chavez', city = 'Merida' WHERE person_id = 1;
UPDATE nombredetabla SET firt_name = 'juan' WHERE city = 'Merida';
UPDATE nombredelatabla SET firt_name = 'juan';

DELETE
DELETE FROM nombredetabla WHERE person_id =1;
DELETE FROM nombreedtabla;

SELECT
SELECT * FROM nombredelatabla;
SELECT first_name, last_name FROM nombredelatabla;
SELECT titulo AS encabezado, fecha,status FROM nombredelatabla; //? aca se le dio un alias a titulo
SELECT COUNT(*) AS numero_deposts FROM nombredetablaposts; //? esto trae todos los post y le da un alias de numero_deposts

FROM 
//uniendo las tablas
JOIN
SELECT * FROM nombredelatabla LEFT JOIN nombredelatabla ON nombredetabla_id = nombredetabla_id; //? vamos a unir las tablas atravez de su id
SELECT * FROM nombredelatabla LEFT JOIN nombredelatabla ON nombredetabla_id = nombredetabla_id WHERE nombredetabla_id IS NULL; // va a traer todos los usuarios que no tengan ningun post
SELECT * FROM nombredelatabla INNER JOIN nombredelatabla ON nombredetabla_id = nombredetabla_id; //INNER trae solo lo que esta internamente ligado

WHERE
SELECT * FROM tabla WHERE id<50;
SELECT * FROM tabla WHERE titulo LIKE %escandalo%; // esto trae todo lo que tenga antes y despues de escandalo
SELECT * FROM tabla WHERE facha_publicacion BETWEEN '2020-01' AND '2021-02';
SELECT * FROM nombredetabla WHERE MOUNT(facha_publicacion) = '04'

```
