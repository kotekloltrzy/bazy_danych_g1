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
select s.nazwa, count(ew.sektor) as ilosc_odwiedzin from sektor s inner join etapy_wyprawy ew on s.id_sektora=ew.sektor group by sektor;
```
##### z funkcją ifnull:
```sql
select s.nazwa, ifnull(count(ew.sektor),'brak') as ilosc_odwiedzin from sektor s inner join etapy_wyprawy ew on s.id_sektora=ew.sektor group by sektor;
```
#### 2) W zależności od ilości wypraw w jakich brała udział dana kreatura wypisz: nazwa kreatury, 'bral udzial w wyprawie' gdy liczba wypraw >0, 'nie bral udzialu w wyprawie' gdy liczba wypraw <0
```sql
select k.nazwa, if(count(u.id_uczestnika)>0, 'bral udzial w wyprawie','nie bral udzialu w wyprawie') as 'czy bral udzial' from uczestnicy u right join kreatura k on k.idKreatury=u.id_uczestnika group by k.nazwa;
```

# Zadanie 4
#### 1) Dla każdej wyprawy wypisz jej nazwe oraz ilośc liczby znaków, które zostały użyte przy pisaniu dziennika, jeśli ta liczba znaków jest mniejsza od 400.
```sql
select w.nazwa, if(sum(length(ew.dziennik))<400,(sum(length(ew.dziennik))),'wiecej niz 400' ) as 'ilosc znakow w dzienniku' from wyprawa w inner join etapy_wyprawy ew on w.id_wyprawy=ew.idWyprawy group by w.nazwa;
```
#### 2) Dla każdej wyprawy podaj średnią wagę zasobów, jakie były niesione przez uczestników tej wyprawy.
```sql
select w.id_wyprawy, w.nazwa,(sum(e.ilosc*z.waga)/(count(u.id_uczestnika))) as 'srednia waga niesiona przez uczestnika' from zasob z inner join ekwipunek e on e.idZasobu=z.idZasobu inner join uczestnicy u on id_uczestnika=e.idKreatury inner join wyprawa w on w.id_wyprawy=u.id_wyprawy group by id_wyprawy;
```

# Zadanie 5
#### 1) Wypisac nazwę kreatury oraz ile miała dni (wiek w dniach) w momencie rozpoczęcia wyprawy, dla wypraw, które przechodziły przez chatkę dziadka
```sql
select k.nazwa, datediff(w.data_rozpoczecia, k.dataUr) from kreatura k inner join uczestnicy u on k.idKreatury=u.id_uczestnika inner join wyprawa w on w.id_wyprawy=u.id_wyprawy inner join etapy_wyprawy ew on w.id_wyprawy=ew.idWyprawy where ew.sektor=7;
```

