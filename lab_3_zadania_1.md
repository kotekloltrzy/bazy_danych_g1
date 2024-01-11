# Zadanie 1 Wyświetl imię i nazwisko każdego pracownika i jego rok urodzenia.
```sql 
select imie, nazwisko, year(data_urodzenia) as 'rok urodzenia' from pracownik;
```
# Zadanie 2 Wyświetl imię i nazwisko pracowników oraz ich wiek w latach (bez uwzględniania miesiąca i dnia urodzenia).
```sql
select imie, nazwisko, (year(current_date())-year(data_urodzenia)) as 'wiek' from pracownik;
```
# Zadanie 3 Wyświetl nazwę działu i liczbę pracowników przypisanych do każdego z nich.
```sql
select d.nazwa, count(p.id_pracownika) as 'ilość pracowników' from dzial d inner join pracownik p on p.dzial=d.id_dzialu group by nazwa;
```
# Zadanie 4 Wyświetl nazwę kategorii oraz liczbę produktów w każdej z nich.
```sql
select k.nazwa_kategori, count(t.kategoria) as 'ilość' from kategoria k inner join towar t on k.id_kategori=t.kategoria group by k.nazwa_kategori;
```
# Zadanie 5 Wyświetl nazwę kategorii i w kolejnej kolumnie listę wszystkich produktów należącej do każdej z nich.
```sql
select k.nazwa_kategori, group_concat(t.nazwa_towaru) as 'produkty' from towar t inner join kategoria k on k.id_kategori=t.kategoria group by t.kategoria;
```
# Zadanie 6 Wyświetl średnie zarobki pracowników za zaokrągleniem do 2 miejsc po przecinku.
```sql
select round(avg(pensja),2) as 'średnia pensja' from pracownik;
```
# Zadanie 7 Wyświetl średnie zarobki pracowników, którzy pracują co najmniej od 5 lat.
```sql
select round(avg(if((year(current_date())-year(data_zatrudnienia))>4, pensja, 0)),2) as 'średnie zarobki pracowników, którzy pracują co najmniej 5 lat' from pracownik;
```
# Zadanie 8 Wyświetl 10 najczęściej sprzedawanych produktów.
```sql
select t.nazwa_towaru, sum(pz.ilosc) as 'ilość sprzedanych kopii'
from pozycja_zamowienia pz inner join towar t on pz.towar=t.id_towaru
group by towar
order by sum(pz.ilosc) desc limit 10;
```
# Zadanie 9 Wyświetl numer zamówienia, jego wartość (suma wartości wszystkich jego pozycji) zarejestrowanych w pierwszym kwartale 2017 roku.
```sql
select z.numer_zamowienia, sum(pz.ilosc*pz.cena) as 'wartość' 
from zamowienie z inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie 
where z.data_zamowienia between '2017-01-01' and '2017-03-31' 
group by z.numer_zamowienia;
```
# Zadanie 10 Wyświetl imie, nazwisko i sumę wartości zamówień, które dany pracownik dodał. Posortuj malejąco po sumie.
```sql
select p.imie, p.nazwisko, sum(pz.ilosc*pz.cena) as 'wartość' 
from zamowienie z inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie inner join pracownik p on p.id_pracownika=z.pracownik_id_pracownika 
group by z.pracownik_id_pracownika 
order by sum(pz.ilosc*pz.cena) desc;
```
