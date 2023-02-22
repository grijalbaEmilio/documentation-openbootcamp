# Variables

## definir/decalrar

```sql
DECLARE
    v_age INTEGER;
    v_salary NUMBER;
    v_name VARCHAR(45):= 'Pepe';
    v_complete BOOLEAN;
```

## seteat
```sql
v_name := 'Juana Marcela'
```

# condicional

## simple if
```sql
IF v_age > 18 THEN 
   DBMS_OUTPUT.PUT_LINE('mayor de edad');
END IF;
```

## with else
```sql
IF v_age >= 18 THEN 
    DBMS_OUTPUT.PUT_LINE('mayor de edad');
ELSE 
    DBMS_OUTPUT.PUT_LINE('menor de edad');
END IF;
```

## with else if/elif/elsif 
```sql
IF v_age >= 18 THEN 
    DBMS_OUTPUT.PUT_LINE('mayor de edad');
ELSIF v_age < 1 THEN
    DBMS_OUTPUT.PUT_LINE('imposible!');
ELSE 
    DBMS_OUTPUT.PUT_LINE('menor de edad');
END IF;
```
