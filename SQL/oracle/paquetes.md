# PAQUETES: PACKAGE
CONTENEDOR DE OBJETOS LÓGICOS 
* variables
* Tipos de datos compuestos
* identificador de los procedimientos almacenados


CABECERA: OBLIGATORIA
CUERPO: NO OBLIGATORIO - DIAGRAMACIÓN LOGICA (SCRIPT) ALMACENADOS

```sql
-- CABECERA:
DROP PACKAGE T2PQ;

CREATE OR REPLACE PACKAGE T2pq AS
TYPE MiTabla IS TABLE OF ESTUDIANTES%ROWTYPE
INDEX BY BINARY_INTEGER;
--VARIABLE INSTANCIA
MiT  MiTabla;
Procedure LlenarT;
 Procedure ImprimirT;

END T2pq;
/

-- CUERPO : BODY

CREATE OR REPLACE PACKAGE BODY T2pq AS
 
Procedure LlenarT 
AS
BEGIN
 for i in (select E.ID, E.APELLIDO||' '||E.NOMBRE as REGISTRO
            from estudiantes e left outer join matriculas m
                 on e.id=m.idestudiante
            where m.idestudiante IS NULL) LOOP
            
 T2pq.MiT(i.ID).ESPECIALIDAD :=I.REGISTRO;

END LOOP;
End Llenart;

Procedure ImprimirT 
as
BEGIN 
DBMS_OUTPUT.PUT_LINE();
end Imprimirt;

END T2pq;
/

begin
t2pq.imprimirT;
END;

-- añadir en el paquete una cunfion retornarT ingresa nFila, retorna las n filas que entran como parámetro
```

```sql
-- package 

CREATE OR REPLACE PACKAGE T2pq
AS


TYPE MyType IS RECORD(
ID ESTUDIANTES%ID,
NOMBRE ESTUDIANTES%NOMBRE,
APELLIDO ESTUDIANTES%APELLIDO,
ESPECIALIDAD ESTUDIANTES%ESPECIALIDAD,
CREDITOS ESTUDIANTES%CREDITOS
);


TYPE MiTabla IS TABLE OF MyType
INDEX BY BINARY_INTEGER;
--VARIABLE INSTANCIA
MiT  MiTabla;

PROCEDURE LlenarT;
-- PROCEDURE Imprimir;
END T2pq;
/
```