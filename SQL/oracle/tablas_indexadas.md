TABLAS INDEXADAS: estructura de datos compuesta (simil a class)

INDEXACION: puentero en memoria cuyo objeto es aumentar el rendimiento en el posicionamiento de búsqueda de información.

BINARY_INTEGER: tipo de dato de alta precisión

# definition

```sql
DECLARE
--COMO DEFINIRLA
TYPE MiTabla IS TABLE OF VARCHAR2(35)
INDEX BY BINARY_INTEGER;
--VARIABLE INSTANCIA
MiT  MiTabla;

BEGIN
MiT(-90000):='karlos';
MiT(978):='fabiola';
MiT(34500):='pablo';
MiT(-3):='juana';

dbms_output.put_line('Numero de Elementos: '||MiT.COUNT);
dbms_output.put_line('Primer Indice:'||MiT.FIRST||' '||'Valor: '||MiT(MiT.FIRST));
--Borrar
MiT.DELETE(MiT.FIRST);
dbms_output.put_line('Numero de Elementos: '||MiT.COUNT);
dbms_output.put_line('Primer Indice: '||MiT.FIRST||' '||'Valor: '||MiT(MiT.FIRST));
dbms_output.put_line('Segundo Indice: '||MiT.NEXT(MiT.FIRST)||' '||'Valor: '||MiT(MiT.NEXT(MiT.FIRST)));
dbms_output.put_line('Ultimo Indice: '||MiT.LAST||' '||'Valor: '||MiT(MiT.LAST));
dbms_output.put_line('PenUltimo Indice: '||MiT.PRIOR(MiT.LAST)||' '||'Valor: '||MiT(MiT.PRIOR(MiT.LAST)));

END;
/
```

```sql
DECLARE
--COMO DEFINIRLA
TYPE MiTabla IS TABLE OF VARCHAR2(35)
INDEX BY BINARY_INTEGER;
--VARIABLE INSTANCIA
MiT  MiTabla;

BEGIN

FOR I IN (SELECT E.ID, E.APELLIDO||' '||E.NOMBRE AS REGISTRO FROM ESTUDIANTES E LEFT OUTER JOIN MATRICULAS M ON E.ID=M.IDESTUDIANTE WHERE M.IDESTUDIANTE IS NULL) LOOP
MiT(I.ID) :=  I.REGISTRO;
END LOOP;

dbms_output.put_line('Numero de Elementos: '||MiT.COUNT);
dbms_output.put_line('Primer Indice:'||MiT.FIRST||' '||'Valor: '||MiT(MiT.FIRST));
--Borrar
MiT.DELETE(MiT.FIRST);
dbms_output.put_line('Numero de Elementos: '||MiT.COUNT);
dbms_output.put_line('Primer Indice: '||MiT.FIRST||' '||'Valor: '||MiT(MiT.FIRST));
dbms_output.put_line('Segundo Indice: '||MiT.NEXT(MiT.FIRST)||' '||'Valor: '||MiT(MiT.NEXT(MiT.FIRST)));
dbms_output.put_line('Ultimo Indice: '||MiT.LAST||' '||'Valor: '||MiT(MiT.LAST));
dbms_output.put_line('PenUltimo Indice: '||MiT.PRIOR(MiT.LAST)||' '||'Valor: '||MiT(MiT.PRIOR(MiT.LAST)));


END;
/

```

```sql

CREATE OR REPLACE PROCEDURE LlenaTabla 
AS
--COMO DEFINIRLA
TYPE MiTabla IS TABLE OF VARCHAR2(35)
INDEX BY BINARY_INTEGER;
--VARIABLE INSTANCIA
MiT  MiTabla;

Puntero1  BINARY_INTEGER;
Puntero2  BINARY_INTEGER;

BEGIN
 for i in (select E.ID, E.APELLIDO||' '||E.NOMBRE as REGISTRO
            from estudiantes e left outer join matriculas m
                 on e.id=m.idestudiante
            where m.idestudiante IS NULL) LOOP
            
 MiT(i.ID) :=I.REGISTRO;

END LOOP;
 

Puntero1:=Mit.FIRST;  
Puntero2:=Mit.LAST;

WHILE Puntero2>=Puntero1 LOOP
dbms_output.put_line('Indice:'|| Puntero2||' '||'Valor:'||MiT(Puntero2));
Puntero2:=Mit.PRIOR(Puntero2);
END LOOP;
 
END LlenaTabla;
/

EXEC LlenaTabla();
```