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
SELECT first_name, last_name FROM people;
```
