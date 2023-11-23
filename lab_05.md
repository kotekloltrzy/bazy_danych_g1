# Zadanie 1
#### Punkt a
```sql
delete from postac where rodzaj="wiking" and nazwa != "Bjorn" order by data_ur asc limit 2;
```
#### Punkt b
```sql
alter table przetwory drop foreign key przetwory_ibfk_1;

alter table walizka drop foreign key walizka_ibfk_1

alter table przetwory drop foreign key przetwory_ibfk_2;

ALTER TABLE postac change id_postaci id_postaci int; # zmienia też nazwę
# lub
ALTER TABLE postac modify id_postaci int;

alter table postac drop primary key;
```
# Zadanie 2
#### Punkt a
```sql
# krok 1
alter table postac add column pesel char(11) first;

# krok 2
update postac set pesel='73947295630' + id_postaci;

# krok 3
alter table postac add primary key(pesel);
```
#### Punkt b
```sql
alter table postac modify rodzaj enum('wiking','ptak','kobieta','syrena');
```
#### Punkt c
```sql
insert into postac values('10174857900', 10, 'Gertuda Nieszczera', 'syrena', default, default, default, default)
```

# Zadanie 3
#### Punkt a
```sql

```
