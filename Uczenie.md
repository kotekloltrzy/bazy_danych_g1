# Tworzenie tabeli
```sql
 create table postac
(id_postaci int primary key auto_increment, 
nazwa varchar(40), 
rodzaj enum("wiking", "ptak", "kobieta"), 
data_ur date, 
wiek int unsigned);
```

# Tworzenie klucza obcego
```sql
create table walizka
(id_walizki int primary key auto_increment,
pojemnosc int unsigned,
kolor enum('rozowy','czerwony','teczowy','zolty'),
id_wlasciciela int,
foreign key(id_wlasciciela) references postac(id_postaci) on delete cascade);
```
# Kilka kluczów głównych
```sql
create table izba
(adres_budynku varchar(100),
nazwa_izby varchar(100),
metraz int unsigned,
wlasciciel int,
primary key(adres_budynku, nazwa_izby),
foreign key(wlasciciel) references postac(id_postaci) on delete set null);
```
# Dodawanie pozycji do tabeli
```sql
insert into postac values(default,'Drozd','ptak','1600-11-09',423);
```
# Aktualizowanie pozycji tabeli
```sql
update postac set wiek=88 where id_postaci=5;
```

