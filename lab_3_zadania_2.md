# Zadanie 1 Wyświetl nazwę działu i minimalną, maksymalną i średnią wartość pensji w każdym dziale.
```sql
select d.nazwa, min(p.pensja) as 'minimalna pensja', max(p.pensja) as 'maksymalna pensja', avg(p.pensja) as 'średnia pensja' from dzial d inner join pracownik p on d.id_dzialu=p.dzial group by p.dzial;
```
# Zadanie 2 Wyświetl pełną nazwę klienta, wartość zamówienia dla 10 najwyższych wartości zamówienia.
```sql

```
