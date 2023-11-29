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
# Ustawianie pozycji domyślnych
```sql
create table przetwory (
id_przetworu INT PRIMARY KEY auto_increment, 
rok_produkcji SMALLINT default "1654", 
id_wykonawcy INT, 
zawartosc VARCHAR(256), 
dodatek VARCHAR(60) default "papryczka chilli",
id_konsumenta INT, 
foreign key (id_wykonawcy) references postac(id_postaci) on delete cascade, 
foreign key (id_konsumenta) references postac(id_postaci) on delete cascade);
```
# Dodawanie kolumn do tabeli
```sql
alter table postac add column funkcja varchar(64);
```
# Usuwanie pozycji z tabeli
```sql
delete from izba where nazwa_izby="spizarnia";
```
# Usuwanie tabeli
```sql
drop table izba;
```
# Bardziej zaawansowane usuwanie pozycji z tabeli
```sql
delete from postac where rodzaj="wiking" and nazwa != "Bjorn" order by data_ur asc limit 2;
```

# Usuwanie klucza głównego
```sql
alter table przetwory drop foreign key przetwory_ibfk_1;
alter table postac modify id_postaci int;
alter table postac drop primary key;
```
# Dodawanie nowego klucza głównego
```sql
# krok 1
alter table postac add column pesel char(11) first;

# krok 2
update postac set pesel='73947295630' + id_postaci;

# krok 3
alter table postac add primary key(pesel);
```

# Edytowanie kolumny typu "enum"
```sql
alter table postac modify rodzaj enum('wiking','ptak','kobieta','syrena');
```
# Postać z literką "a" w nazwie
```sql
update postac set statek='zaglowiec' where nazwa like '%a%';
```
# Zmniejszenie ładowności o 30% u statków utworzonych między konkretnymi latami 
```sql
update statek set max_ladownosc=max_ladownosc * 0.7 where year(data_wodowania) between 1901 and 2000;
```
# Zablokowanie dodawania postaci starszych niż 1000 lat
```sql
alter table postac add check(wiek <= 1000);
```
# Tworzenie tabeli identycznej do innej
#### Utworzenie tabli
```sql
create table marynarz like postac;
```
#### Przekopiowanie postaci z statkim do nowej tabeli
```sql
insert into marynarz select * from postac where statek is not NULL;
```
#### Ustawienie PESELu jako klucz główny w nowej tabeli
```sql
alter table marynarz add primary key(pesel);
```
# Ustawinie wszystkich pozycji na domyślną
```sql
update postac set statek=default;
```
# Usunięcie wszystkich pozycji z tabeli
```sql
delete from statek;
```
# Skopiowanie do tabeli konkrete pozycje
```sql
insert into zwierz select id_postaci, nazwa, wiek from postac where rodzaj='ptak' or rodzaj='syrena' or rodzaj='waz';
```
