# Zadanie 1
## Punkt a
```sql
delete from postac where rodzaj="wiking" and nazwa != "Bjorn" order by data_ur asc limit 2;

alter table postac drop primary key;

ALTER TABLE postac change id_postaci id_postaci int; # zmienia też nazwę
# lub
ALTER TABLE postac modify id_postaci int;

```
## Punkt b
```sql

```
