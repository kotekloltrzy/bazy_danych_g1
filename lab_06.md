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
# Zadanie 2
#### 1)
```sql
select * from kreatura where rodzaj <> 'wiedzma' and udzwig >= 50;
```
#### 2)
```sql
select * from zasob where waga between 2 and 5;
```
#### 3)
```sql
select * from kreatura where nazwa like '%or%' and waga between 30 and 70;
```
# Zadanie 3
#### 1)
```sql
select * from zasob where month(dataPozyskania) between 8 and 9;
```
#### 2)
```sql
select * from zasob order by waga;
```
#### 3)
```sql
select * from kreatura where dataUr is not Null order by dataUr limit 5;
```
# Zadanie 4
#### 1)
```sql
select distinct rodzaj from zasob;
```
#### 2)
```sql
select concat(nazwa,' ',rodzaj) as 'nazwa rodzaj' from kreatura where rodzaj like 'wi%';
```
#### 3)
```sql
select idZasobu, nazwa, waga*ilosc as calkowita_waga, dataPozyskania, rodzaj from zasob where year(dataPozyskania) between 2000 and 2007;
```
# Zadanie 5
#### 1)
```sql
select idZasobu, nazwa, waga*0.7*ilosc as wlasciwe_jedzenie, waga*0.3*ilosc as odpadki_jedzenia, dataPozyskania, rodzaj from zasob where rodzaj = 'jedzenie';
```
#### 2)
```sql
select * from zasob where rodzaj is Null;
```

#### 3)
```sql
select distinct * from zasob where nazwa like 'Ba%' or '%os' order by nazwa;
```

