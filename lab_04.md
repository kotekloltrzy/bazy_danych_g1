# Zadanie 1
```sql
create table postac ( id_postaci int primary key auto_increment, nazwa varchar(40) not null,
rodzaj enum('wiking', 'ptak', 'kobieta'), data_ur date, wiek int unsigned);

insert into postac values (default,"Bjorn","wiking","1700-10-23",23);

insert into postac values(default,"Drozd","ptak","1540-10-23",234);

insert into postac values(default,"Tesciowa","kobieta","1-01-01",234);

update postac set wiek=88 where id_postaci=5;
```
# Zadanie 2
```sql
create table walizka(id_walizki int primary key auto_increment, pojemnosc int unsigned,
kolor enum("rozowy", "czerwony", "teczowy", "zolty"), id_wlasciciela int,
foreign key (id_wlasciciela) references postac(id_postaci) on delete cascade);

alter table walizka alter kolor set default "rozowy";

insert into walizka values(default,100,"zolty",1);
```
# Zadanie 3
```sql
create table izba( adres_budynku varchar(40), nazwa_izby varchar(40),
primary key(adres_budynku, nazwa_izby),
metraz int unsigned,
id_wlasciciela int,
foreign key (id_wlasciciela) references postac(id_postaci) on delete set null);

ALTER TABLE izba ADD COLUMN kolor_izby enum("rozowy","zolty","bialy") AFTER metraz;

insert into izba values("Chatka Bjorna","Spizarnia", 20, "bialy", 1);
```
# Zadanie 4
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

insert into przetwory values(default, default, 1, "bigos", default, 2);
```
# Zadanie 5

```sql
insert into postac values(default, "Adam", "wiking", "2002-12-12" , 21);
insert into postac values(default, "Marcel", "wiking", "2002-11-04" , 21);
insert into postac values(default, "Tomek", "wiking", "2002-05-06" , 21);
insert into postac values(default, "Kuba", "wiking", "2002-01-13" , 21);
insert into postac values(default, "Michal", "wiking", "2003-05-08" , 20);

create table statek (
nazwa_statku varchar(256) PRIMARY KEY,
rodzaj_statku INT,
data_wodowania DATE,
max_ladownosc INT unsigned);

insert into statek values("zaglowiec", 1, "2020-06-23", 1000);
insert into statek values("jacht", 2, "2023-06-16", 2000);

alter table postac add column funkcja varchar(64);

update postac set funkcja="kapitan" where id_postaci=1;

alter table postac add column statek varchar(256);

update postac set statek="zaglowiec" where id_postaci=1;
update postac set statek="zaglowiec" where id_postaci=2;
update postac set statek="jacht" where id_postaci=5;
update postac set statek="jacht" where id_postaci=6;
update postac set statek="jacht" where id_postaci=7;
update postac set statek="jacht" where id_postaci=8;
update postac set statek="jacht" where id_postaci=9;

delete from izba where nazwa_izby="spizarnia";
drop table izba;
```
