# Nagłówek 1
## Nagłówek 2
### Nagłówek 3
#### Nagłówek 4
##### Nagłówek 5
###### Nagłówek 6

**Pogrubiony** tekst...  
**_Pogrubiony i kursywa_** ...  

**Listing 1**

Na tym listingu...

```sql
SELECT * FROM osoba;
```

Kod mozemy umieścić liniowo czyli `SELECT * FROM osoba;` tak

Lista uporządkowana (numerowana).
1. Pozycja 1.  
2. Pozycja 2.  
2.1 Pozycja 2.1

Lista wypunktowana:
* punkt 1
* punkt 2
  * punkt 2.1
 
[link](url) -> link  
![obraz](url) -> obraz  

```sql
 create table postac
(id_postaci int primary key auto_increment, 
nazwa varchar(40), 
rodzaj enum("wiking", "ptak", "kobieta"), 
data_ur date, 
wiek int unsigned);
```

```sql
create table walizka
(id_walizki int primary key auto_increment,
pojemnosc int unsigned,
kolor enum('rozowy','czerwony','teczowy','zolty'),
id_wlasciciela int,
foreign key(id_wlasciciela) references postac(id_postaci) on delete cascade);
```
```sql
create table izba
(adres_budynku varchar(100),
nazwa_izby varchar(100),
metraz int unsigned,
wlasciciel int,
primary key(adres_budynku, nazwa_izby),
foreign key(wlasciciel) references postac(id_postaci) on delete set null);
```
```sql
insert into walizka values(default,50,'teczowy',3);
```

```sql
insert into walizka values(default,50,default,1);
```

```sql
insert into izba values('Nad rzeka', 'spizarnia', 6, default, '1');
```

```sql
insert into postac values(default,'Drozd','ptak','1600-11-09',423);
```
