# Zadanie 1
#### 1) wyświetl średnią wagę wszystkich wikingów
```sql
select avg(waga) as srednia_waga from kreatura where rodzaj = 'wiking';
```
#### 2) wyświetl średnią wagę oraz lliczbę kreatur dla każdego rodzaji
```sql
select rodzaj, avg(waga) as srednia_waga, count(*) as ilosc_kreatur from kreatura where rodzaj is not Null group by rodzaj;
```
#### 3) wyświetl średni wiek dla każdego rodzaju kreatury
```sql
select rodzaj, round(avg(year(curdate())-year(dataUr)), 2) as sredni_wiek from kreatura where rodzaj is not Null group by rodzaj;
```
# Zadanie 2
#### 1) dla każdego rodzaju zasobu wyświetlić sume wag tego zasobu
```sql
select rodzaj, sum(waga*ilosc) as suma_wag from zasob group by rodzaj;
```
#### 2) dla każdej nazwy zasobu wyświetlić średnią wagę, jeśli ilośc jest równa co najmniej 4 oraz jeśli ta suma wag jest większa od 10
```sql
select nazwa, avg(waga) from zasob where ilosc >= 4 group by nazwa having sum(waga) > 10;
```
#### 3) wyświetlić ile jest różnych nazw dla każdego rodzaju zasobu, jesli minimalna ilość zasobu jest większa od 1
```sql
select rodzaj, count(distinct nazwa) as ilosc_unikalnych_nazw from zasob group by rodzaj having min(ilosc) > 1;
```
# Zadanie 3
#### 1) wyswietl dla każdej kreatury ilość zasobów jakie niesie
```sql
select k.nazwa, sum(e.ilosc) as ilosc_zasobow from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury group by k.nazwa;
```
#### 2) wyswietlic dla kazdej kreatury nazwy zasobow jakie posiada
```sql
select k.nazwa, z.nazwa from kreatura k inner join ekwipunek e inner join zasob z on k.idKreatury=e.idKreatury and e.idZasobu=z.idZasobu;
```
#### 3) wyświetlić kreatury które nie posiadają żadnego ekwipunku
```sql
select k.nazwa from kreatura k left join ekwipunek e on k.idKreatury=e.idKreatury where e.idKreatury is null;
```
#### lub
```sql
select nazwa, idKreatury from kreatura where idKreatury not in (select distinct idKreatury from ekwipunek where idKreatury is not null);
```
# Zadanie 4
#### 1) wyswietlić nazwy wikingów , ktorzy urodzili sie w latach 70-tych XVII wieku oraz nazwy zasobów, które posiadają (użyj natural joina jeśli się da)
```sql
select k.nazwa, z.nazwa from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury inner join zasob z on e.idZasobu=z.idZasobu where k.rodzaj = "wiking" and k.dataUr between 1770 and 1779;
```
#### 2) wyświetlic nazwy 5 najmłodszych kreatur, które w ekwipunku posiadają jedzenie
```sql
select k.nazwa from kreatura k inner join ekwipunek e on k.idKreatury=e.idKreatury inner join zasob z on e.idZasobu=z.idZasobu where z.rodzaj = "jedzenie" order by k.dataUr desc limit 5;
```
#### 3) wypisz obok siebie nazwy kreatur, których numer idKreatury różni się o 5 (np Bjorn - Astrid, Brutal Ibra itd)
```sql

```
