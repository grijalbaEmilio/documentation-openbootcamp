# Cursores 

cursores: Conjunto de filas resulstantes de una operación de cunsulta a un modelo relacional o de una operacion DML(insert, update, delete), para recorrerlos se usa Bucles de extración.

Principio fila 1
Final     Ultima Fila

Implicitos: se da cuando se ejecuta una consulta normal
Explisitos: tienen un identificador en memoria --> Operación Query

Parametrizados
RefCursor

## Funciones
1. `SQL%FOUND `(retorna booleano), retorna `True` si el cursor encontró filas, `False` en otro caso.
2. `SQL%NOTFOUND` (retorna booleano), retorna `True` si el cursor no encontró filas, `False` en otro caso.
3. `SQL%ROWCOUNT` (retorna entero) devuelve el numero de filas procesadas por el cursor
4. `SQL%ISOPEN` (booleano) True si el cursor está abierto

en caso que se procese un cursor explicito entonces la palabra reservada SQL se reemplaza por el identificador del cursor


## con for
```sql
DECLARE 
CURSOR MIC IS SELECT DISTINCT(E.ID ||' '||E.NOMBRE||' '||E.APELLIDO) INFO
FROM ESTUDIANTES E 
INNER JOIN MATRICULAS M 
ON E.ID=M.IDESTUDIANTE;

BEGIN
DELETE FROM TEMPORAL;
FOR I IN MIC LOOP
INSERT INTO TEMPORAL(COLUMNACARACTER)
VALUES(I.INFO);
END LOOP;
END;
```

## con loop
```sql
DECLARE
    CURSOR MIC IS SELECT DISTINCT(E.ID||' '||E.NOMBRE||' '||E.APELLIDO||' '||E.ESPECIALIDAD||' '||TO_CHAR(E.CREDITOS)) INFO
                   FROM ESTUDIANTES E INNER JOIN MATRICULAS M
                        ON E.ID=M.IDESTUDIANTE;
                        
Total INTEGER:=0;  
SALIDA VARCHAR2(120);
BEGIN
DELETE FROM TEMPORAL;
OPEN MIC;


LOOP
FETCH MIC INTO SALIDA;
EXIT WHEN MIC%NOTFOUND;

INSERT INTO TEMPORAL(COLUMNACARACTER)
VALUES(SALIDA);
END LOOP;
 
DBMS_OUTPUT.PUT_LINE('TOTAL:'||MIC%ROWCOUNT);
CLOSE MIC;
END;
/
```

## con while
```sql
DECLARE
    CURSOR MIC IS SELECT DISTINCT(E.ID||' '||E.NOMBRE||' '||E.APELLIDO||' '||E.ESPECIALIDAD||' '||TO_CHAR(E.CREDITOS)) INFO
                   FROM ESTUDIANTES E INNER JOIN MATRICULAS M
                        ON E.ID=M.IDESTUDIANTE;
                        
Total INTEGER:=0;  
SALIDA VARCHAR2(120);
BEGIN
DELETE FROM TEMPORAL;
OPEN MIC;
 FETCH MIC INTO SALIDA;
 WHILE MIC%FOUND LOOP

INSERT INTO TEMPORAL(COLUMNACARACTER)
VALUES(SALIDA);
  FETCH MIC INTO SALIDA;

END LOOP;
 
DBMS_OUTPUT.PUT_LINE('TOTAL:'||MIC%ROWCOUNT);
CLOSE MIC;
END;
/
```