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
delimiter //
create procedure eliksir_sily (in id int)
begin
	update kreatura set udzwig = udzwig*1.2 where idKreatury = id;
end//

delimiter ;
```
#### 2) Napisz funkcję, która będzie pobierała tekst i zwracała go z wielkich liter
```sql
delimiter $$
create procedure duze_litery (in tekst varchar(255))
begin
	select upper(tekst);
end$$

delimiter ;
```

# Zadanie 4
#### 1) Stwórz tabelę "system alarmowy" z polami, id_alarmu, wiadomosc.
```sql
create table system_alarmowy(id_alarmu int primary key auto_increment, wiadomosc varchar(100));
```
#### 2) Dodaj wyzwalacz, który będzie sprawdzał czy w tabeli wyprawy pojawiła się misja, w której bierze udział teściowa oraz czy jednym z sektorów misji jest domek dziadka, Jeżeli w/w zaistnieje wyzwalacz wstawi rekord do tabeli "system_alarmowy" z treścią "Teściowa nadchodzi"
```sql
DELIMITER $$

CREATE TRIGGER uczestnicy_after_insert
AFTER INSERT ON uczestnicy
FOR EACH ROW
BEGIN
	DECLARE tesciowa varchar(100);
	DECLARE sektor_id integer;
	DECLARE czy_tesciowa bool;
	DECLARE czy_chata_dziadka bool;
	SET tesciowa = 'Tesciowa';
	SET sektor_id = 7;
	
/** sprawdzanie czy tesciowa bierze udział w wyprawie **/
    
IF tesciowa in (
	SELECT nazwa from kreatura WHERE idKreatury in 
	( SELECT id_uczestnika from uczestnicy where id_wyprawy=NEW.id_wyprawy)) 
	
THEN 
    
	SET czy_tesciowa = true;
	END IF;
    
IF sektor_id in (
	SELECT sektor FROM etapy_wyprawy WHERE idWyprawy=NEW.id_wyprawy
	) 
THEN 
	SET czy_chata_dziadka = true;
END IF;
    
IF czy_tesciowa AND czy_chata_dziadka
    
THEN  
	INSERT INTO system_alarmowy VALUES(default,'Tesciowa nadchodzi',default);
END IF;

END
$$

DELIMITER ;
```
