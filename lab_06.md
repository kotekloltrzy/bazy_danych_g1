# Zadanie 1
#### 1)
```sql
create table infs_brodam.kreatura as select * from wikingowie.kreatura;
```
```sql
create table infs_brodam.zasob as select * from wikingowie.zasob;
```

```sql
create table infs_brodam.ekwipunek as select * from wikingowie.ekwipunek;
```
#### 2)
```sql
select * from zasob;
```
#### 3)
```sql
select * from zasob where rodzaj='jedzenie';
```
#### 4)
```sql
select idZasobu, ilosc from ekwipunek where idKreatury = 1 or 3 or 5;
```
