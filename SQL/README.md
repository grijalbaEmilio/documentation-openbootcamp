# creacion

## crear database
```sql
	CREATE DATABASE IF NOT EXISTS name_database;
```
## crear tablas
```sql
	CREATE TABLE IF NOT EXISTS name_table(
		id INT NOT NUL AUTO_INCREMENT UNIQUE
	);
```
## especificar id
```sql
	CONSTRAINT pk_user PRIMARY KEY(id);
```
## especificar clave foránea
```sql
	CONSTRAINT fk_user_comment FOREIGN KEY(id_comment) REFERENCE comment(id) ON UPDATE CASCADE ON DELETE CASCACDE;
```
## borrar tabla
```sql
	DROP TABLE IF EXISTS 
```
## agregar columna a tabla
```sql
	ALTER TABLE name_table ADD COLUMN email VARCHAR(40);
```
## borrar comumna a tabla
```sql
	ALTER TABLE name_table DROP COLUMN email;
```
## cambiar nombre de tabla
```sql
	ALTER TABLE name_table RENAME TO new_name_table;
```
## tipos de datos en las tablas
```sql
	INT 
	VARCHAR(length)
	DATE
	CHAR
	BOOLEAN
	TEXT
	NUMERIC(capacityInt, capacityDecimal)
``` 	
## restricciones
```sql
	PRIMARY KEY
	NOT NULL
	AUTO_INCREMENT
	UNIQUE 
	CHECK(age > 0)
```
# consultas DML

## insertar datos
```sql
	INSERT INTO name_database(id)
	VALUES
	(1),
	(2);
```
## actualizar un registro | RETURNING devuelve los registros actualizados
```sql
	UPDATE user_tbl SET age = 50 where id = 2;
	UPDATE user_tbl SET age = 50, name = "pepe" where id = 2 RETURNING *;
```
## eliminar registros
```sql
 	DELETE FROM user_tbl;
	DELETE FROM user_tbl WHERE id = 3;
```
## todos los campos 
```sql
	SELECT * FROM name_database;
```
## campos sin repeticion | distintos
```sql
	SELECT DISTINCT name FROM user_tbl;
```
## campos determinados 
```sql
	SELECT name, email FROM user_tbl;
```
## nombre determinado 
```sql
	SELECT name, email FROM user_tbl
	WHERE name = "Luis Emilio";
```
## exceptuar
```sql
	SELECT * FROM user_tbl WHERE name = "Luis Emilio";
	SELECT * FROM user_tbl WHERE name = "Luis Emilio";
	SELECT * FROM user_tbl WHERE NOT name = "Luis Emilio";
```
## varias condiciones
```sql
	SELECT name, email FROM user_tbl
	WHERE name = "Luis Emilio"
	AND salary > 10000;
```
## condiciones de coincidencia abrebiada
```sql
	SELECT name FROM user_tbl
	WHERE name IN("Luis", "Carlos", "Oscary");
```
## filtrar
```sql
	SELECT * FROM user_tbl FROM name LIKE "A%"; -- inicia con A
	SELECT * FROM user_tbl FROM name LIKE "%A"; -- finaliza con A
	SELECT * FROM user_tbl FROM name LIKE "%A%"; -- contiene A
```
## ordenat
```sql
	SELECT * FROM user_tbl FROM name LIKE "A%"
	ORDER BY age;
```
## agrupar
```sql
	SELECT age, COUNT(age) as repeatNum FROM user_tbl FROM name LIKE "A%"
	GROUP BY age;
```
## filtrar por condicion de función | HAVING
```sql
	SELECT name, COUNT(name) FROM user_tbl 
	GROUP BY(name)
	HAVING COUNT(name) > 1;
```
## JOIN
```sql
	SELECT usr.name, usr.age, cmn.title FROM user_tbl AS usr
	INNER JOIN comment_tbl AS cmn
	ON user_tbl.comment_id == comment_tbl.id
	WHERE user_tbl.name = "Luis Emilio";
```
# SUBQUERY
```sql
	SELECT title FROM film
	WHERE language_id IN (SELECT language_id FROM language WHERE name = 'English' or name = 'Italian')
```
# Stored Procedure

## creación	

```sql
	DELIMITER $$
	CREATE PROCEDURE query_names(IN name_filter VARCHAR(50), OUT result INT)
	BEGIN
		SELECT COUNT(name) INTO result FROM user_tbl
	    WHERE name = name_filter
	    GROUP BY name;
	END $$
```
## llamado
```sql	
	CALL query_names("Lui Emili", @result);
	SELECT @result AS "color vehículo";
```