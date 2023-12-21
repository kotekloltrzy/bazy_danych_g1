# Zadanie 1
#### 1) Wypisz nazwy kreatur które nie uczestniczyły w żadnej wyprawie
```sql
select k.nazwa from kreatura k left join uczestnicy u1 on k.idKreatury=u1.id_uczestnika where u1.id_uczestnika is null;
```
#### 2) Dla każdej wyprawy wypisać jej nazwę oraz sumę ilości ekwipuinku, jaka została zabrana przez uczestników tej wyprawy.
```sql
select w.nazwa, sum(e.ilosc) as suma_iloci_ekwipunku from wyprawa w left join uczestnicy u on w.id_wyprawy=u.id_wyprawy left join kreatura k on u.id_uczestnika=k.idKreatury left join ekwipunek e on k.idKreatury=e.idKreatury group by w.id_wyprawy;
```

# Zadanie 2
#### 1) Dla każdej wyprawy wypisz jej nazwę, liczbę uczestników, oraz nazwy tych uczestników w jednej lini
```sql
select w.nazwa, count(u.id_uczestnika) as ilosc_uczestnikow, group_concat(k.nazwa) from wyprawa w left join uczestnicy u on w.id_wyprawy=u.id_wyprawy inner join kreatura k on k.idKreatury=u.id_uczestnika group by w.id_wyprawy;
```
#### 2)
```sql
select s.nazwa, w.data_rozpoczecia, e.kolejnosc, k.nazwa as kierownik from etapy_wyprawy e inner join wyprawa w on e.idWyprawy=w.id_wyprawy inner join kreatura k on k.idKreatury=w.kierownik join sektor s on e.sektor=s.id_sektora order by w.data_rozpoczecia asc, e.kolejnosc;
```
# Zadanie 3
#### 1) Wypisać ile razy dany sektor był odwiedzany w trackie wyprawy
```sql

```
