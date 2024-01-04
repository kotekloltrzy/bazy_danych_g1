# Zadanie 1
#### 1) Napisz wyzwalacz, który przed wstawieniem lub modyfikacją tabeli kreatura sprawdzi czy waga jest większa od zera
```sql
delimiter //
create trigger kreatura_before_insert_waga
before insert on kreatura
for each row
begin
	if new.waga <= 0
	then
		set new.waga = 1;
	end if;
	end //
delimiter ;
```
# Zadanie 2
#### 1)
```sql
delimiter //
create trigger wyprawa_before_delete
before delete on wikingowie.wyprawa
for each row
	begin
		insert into infs_brodam.archiwum_wypraw
		(id_wyprawy, nazwa, data_rozpoczecia, data_zakonczenia, kierownik)
        values(old.id_wyprawy, old.nazwa, old.data_rozpoczenia, old.data_zakonczenia, old.kierownik);
	end //

delimiter ;
```

# Zadanie 3
#### 1) Napisz procedurę o nazwie "eliksir siły", która będzie podnosiła wartość udzwig z tabeli kreatura o 20% na podstawie id_kreatury przekazywanego jako parametr.
```sql

```
#### 2) Napisz funkcję, która będzie pobierała tekst i zwracała go bez wielkich liter
```sql

```
