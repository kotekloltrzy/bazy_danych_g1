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

end
//
delimiter ;
```
