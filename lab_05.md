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
update postac set statek='zaglowiec' where nazwa like '%a%';
```

#### Punkt b

```sql
update statek set max_ladownosc=max_ladownosc * 0.7 where year(data_wodowania) between 1901 and 2000;
```

#### Punkt c

```sql
alter table postac add check(wiek <= 1000);
```

# Zadanie 4

#### Punkt a

```sql
alter table postac modify rodzaj enum('wiking','ptak','kobieta','syrena', 'waz');

insert into postac values('23456819511', 11, 'Loko', 'waz', default, 960, default, default);
```

#### Punkt b

```sql
create table marynarz like postac;

insert into marynarz select * from postac where statek is not NULL;
```

#### Punkt c

```sql
alter table marynarz add primary key(pesel);
```

# Zadanie 5

#### Punkt a

```sql
update postac set statek=default;
```

#### Punkt b

```sql
delete from postac where rodzaj='wiking' and nazwa != 'Bjorn' order by id_postaci asc limit 1;
```

#### Punkt c

```sql
delete from statek;
```

#### Punkt d

```sql
drop table statek;
```

#### Punkt e

```sql
create table zwierz (id_zwierza int primary key auto_increment not null, nazwa varchar(60), wiek int);
```

#### Punkt f

```sql
insert into zwierz select id_postaci, nazwa, wiek from postac where rodzaj='ptak' or rodzaj='syrena' or rodzaj='waz';
```
