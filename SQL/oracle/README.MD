PL/SQL: procedural orientado a objetos. Incorporando al paquete comercial de Oracle. Empaqueter unidades de trabajo logica para que sean procesados de una sola manera.

Bloque: codigo script en lenguaje DDL, DML, DSL ordenado logicamente que cumple algun tipo de objetivo.
Anonimos: No puede ser invocado
Nominados: Si puede ser invocado porque corresponde a un objeto

Plantilla PL/SQL: 
```sql
SET SETSERVEROUTPUT ON;

DECLARE
	-- zona declaracion variables
	-- No obligatorio
	Vnombre VARCHAR(50):= 'Mauricio';
	Vestatura NUMBER(3,2):= 1.90;
BEGIN
	-- zona de ejecución
	-- Operaciones DML(insert, update, delete)
	-- extracciones materiales de querys, invocaciones a otros
	-- programas, cambio de estado de variables etc.
	DBMS_OUTPUT.PUT_LINE('Nombre:'||Vnombre||' Estatura:'||Vestatura);

EXCEPTION
	-- Zona de tratamiento de errores
	-- No obligatoria
END;
```
## print in DBMS 

```sql
DBMS_OUTPUT.PUT_LINE('literal text' || v_variable);
```