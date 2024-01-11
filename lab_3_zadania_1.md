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
