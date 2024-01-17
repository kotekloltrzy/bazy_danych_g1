# Zadanie 1 Wyświetl nazwę działu i minimalną, maksymalną i średnią wartość pensji w każdym dziale.
```sql
select d.nazwa, min(p.pensja) as 'minimalna pensja', max(p.pensja) as 'maksymalna pensja', avg(p.pensja) as 'średnia pensja'
from dzial d inner join pracownik p on d.id_dzialu=p.dzial group by p.dzial;
```
# Zadanie 2 Wyświetl pełną nazwę klienta, wartość zamówienia dla 10 najwyższych wartości zamówienia.
```sql
select k.pelna_nazwa, (pz.ilosc*pz.cena) as "wartość zamówienia"
from klient k inner join zamowienie z on z.klient=k.id_klienta inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie
order by (pz.ilosc*pz.cena) desc limit 10;
```
# Zadanie 3 Wyświetl wartość przychodu dla każdego roku. Dane posortuj malejąco według sumy wartości zamówień.
```sql
select year(z.data_zamowienia) as "rok", sum(pz.ilosc*pz.cena) as "przychód roczny"
from zamowienie z inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie 
group by year(z.data_zamowienia) order by sum(pz.ilosc*pz.cena) desc;
```
# Zadanie 4 Wyświetl sumę wartości wszystkich anulowanych zamówień.
```sql
select sum(pz.towar*pz.cena) as "łączna wartość anulowanych zamówień" 
from zamowienie z inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie 
where z.status_zamowienia="6";
```
# Zadanie 5 Wyświetl liczbę zamówień i sumę zamówień dla każdego miasta z podstawowego adresu klientów.
```sql
select ak.miejscowosc, count(z.id_zamowienia) as "ilość zamówień", sum(pz.ilosc*pz.cena) as "suma wartośći zamówień"
from zamowienie z inner join adres_klienta ak on z.klient=ak.klient inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie 
group by ak.miejscowosc;
```
# Zadanie 6
```sql

```
