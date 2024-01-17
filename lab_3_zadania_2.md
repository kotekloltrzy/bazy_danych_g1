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
# Zadanie 6 Wyświetl dotychczasowy dochód firmy biorąc pod uwagę tylko zamówienia zrealizowane.
```sql
from zamowienie z inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie where z.status_zamowienia="5";
```
# Zadanie 7 Policz i wyświetl dochód (przychód z zamówień i cena zakupu towaru) w każdym roku działalności firmy.
```sql
select year(z.data_zamowienia) as "rok", sum(pz.ilosc*(pz.cena-t.cena_zakupu)) as "dochód roczny"
from zamowienie z inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie inner join towar t on pz.towar=t.id_towaru
group by year(z.data_zamowienia) order by sum(pz.ilosc*pz.cena) desc;
```
# Zadanie 8 Wyświetl wartość aktualnego stanu magazynowego z podziałem na kategorię produktów.
```sql
select k.nazwa_kategori, sum(t.cena_zakupu*sm.ilosc) as "wartość kategorii" 
from stan_magazynowy sm inner join towar t on sm.towar=t.id_towaru inner join kategoria k on t.kategoria=k.id_kategori
group by t.kategoria;
```
# Zadanie 9 Przygotuj zapytanie, które wyświetli dane w poniższej postaci (policz ilu pracowników urodziło się w danym miesiącu - uwaga na porządek sortowania).
```sql
select monthname(data_urodzenia) as miesiac, count(id_pracownika) as ilu 
from pracownik group by miesiac order by min(month(data_urodzenia)) asc;
```

# Zadanie 10* Wyświetl imię i nazwisko pracownika i koszt jaki poniósł pracodawca od momentu jego zatrudnienia.

    Nie aż tak trudne jak poszukać odpowiedniej funkcji operującej na datach.

```sql
select imie, nazwisko, (((((year(current_date())-year(data_zatrudnienia))*12)+month(current_date()))-month(data_zatrudnienia))*pensja) as "koszty zatrudnienia" from pracownik;
```
