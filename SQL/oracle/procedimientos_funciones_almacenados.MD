# Procedimentos almacenados

`Def`: hacen parte de la base de datos

Procedure
Function --> return (escalar o compuesto)

## plantilla
### PROCEDIMIENTOS
```sql
-- parametros
-- IN  ENTRADA             SÓLO LECTUR        DEFAULT
-- OUT SALIDA			   SÓLO ESCRITURA
-- IN  OUT ENTRADA/SALIDA  LECTURA/ESCRITURA

CREATE <OR REPLACE> PROCEDURE <identificador>
-- parametros
(P1 <IN, OUT, IN OUT> <tipo_escalar> <DEFAULT value>,
 P2 <IN, OUT, IN OUT> <tipo_escalar> <DEFAULT value>)

-- AS/IS reemplaza a DECLARE
AS/IS
-- variables compuestas o escalares

BEGIN

-- EXCEPTION
END <identificador>;
show error
```

invocación
```sql
-- procedimientos
EXECUTE <identificador(P1, P2, Pn)>

BEGIN
Identificador(P1, P2, Pn)
END;
```

### FUNCIONES
```sql
-- parametros
-- IN  ENTRADA             SÓLO LECTUR        DEFAULT
-- OUT SALIDA			   SÓLO ESCRITURA
-- IN  OUT ENTRADA/SALIDA  LECTURA/ESCRITURA

CREATE <OR REPLACE> FUNCTION <identificador>
-- parametros
(P1 <IN, OUT, IN OUT> <tipo_escalar> <default>,
 P2 <IN, OUT, IN OUT> <tipo_escalar> <default>)

RETURN
<tipo_retorno_sin_longitud>

-- AS/IS reemplaza a DECLARE
AS/IS
-- variables compuestas o escalares

BEGIN

RETURN <VARIABLE_ASOCIADA>

-- EXCEPTION
END <identificador>;
show error
```

invocación
```sql
-- Usando una query a la BD
-- Usando un bloque anónimo cun una variable que tenga el mismo tipo de retorno

SELECT <Identificador_funciion>(P1, P2, Pn) AS <ALIAS>, Columna2, ColumnaN
FROM Dual
<WHERE>
<GROUP BY>

BEGIN
Identificador(P1, P2, Pn)
END;
```