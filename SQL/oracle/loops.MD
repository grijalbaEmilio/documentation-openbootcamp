# SIMPLE LOOP
```sql
LOOP
    -- must be declare v_sum
    v_sum := v_sum + 1;
    IF v_sum > 10 THEN
        EXIT;
    END IF;
    DBMS_OUTPUT.PUT_LINE('sum is: '||v_sum);
END LOOP;
```

# WILE
```sql
WHILE v_sum < 11 LOOP
    v_sum := v_sum + 1;
END LOOP;
DBMS_OUTPUT.PUT_LINE(v_sum);
```

# FOR
```sql
-- no must be declare v_count
FOR v_count in 0 .. 5
    LOOP
    DBMS_OUTPUT.PUT_LINE('counter is: '||v_count);
    END LOOP;
```