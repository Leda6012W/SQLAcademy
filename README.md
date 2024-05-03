##### SQL Academy
Решения задач из тренажёра [SQL Academy](sql-academy.org).

**Задание 1.** Вывести имена всех людей, которые есть в базе данных авиакомпаний

<details>
	<summary>Решение</summary>
	
``` sql
SELECT name FROM Passenger
```

</details>

**Задание 2.** Вывести названия всеx авиакомпаний
<details>
	<summary>Решение</summary>

 ``` sql
SELECT name
FROM Company
```

</details>

**Задание 3.** Вывести все рейсы, совершенные из Москвы
<details>
	<summary>Решение</summary>

 ``` sql
SELECT *
FROM Trip
WHERE town_from = 'Moscow';
```

</details>

**Задание 4.** Вывести имена людей, которые заканчиваются на "man"
<details>
	<summary>Решение</summary>

 ``` sql
SELECT name
FROM Passenger
WHERE name LIKE '%man'
```
 
</details>

**Задание 5.** Вывести количество рейсов, совершенных на TU-134
<details>
	<summary>Решение</summary>

 ``` sql
SELECT COUNT(*) as count
FROM Trip
WHERE plane = 'TU-134'
```

</details>

**Задание 6.** Какие компании совершали перелеты на Boeing
<details>
	<summary>Решение</summary>

 ``` sql
SELECT DISTINCT name
FROM Trip
	JOIN Company on Trip.company = Company.id
WHERE plane = 'Boeing';
```

</details>

**Задание 7.** Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)
<details>
	<summary>Решение</summary>

  ``` sql
SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'
```

</details>

**Задание 8.** В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?
<details>
	<summary>Решение</summary>

  ``` sql
SELECT town_to,
	TIMEDIFF(time_in, time_out) as flight_time
from Trip
WHERE town_from = 'Paris'
```

</details>

**Задание 9.** Какие компании организуют перелеты из Владивостока (Vladivostok)?
<details>
	<summary>Решение</summary>

  ``` sql
SELECT Company.name
from Trip
	INNER JOIN Company on Trip.company = Company.id
WHERE town_from = 'Vladivostok'
```

</details>

**Задание 10.** Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.
<details>
	<summary>Решение</summary>

  ``` sql
SELECT *
FROM Trip
WHERE DATE(time_out) = '1900-01-01'
	AND TIME(time_out) BETWEEN '10:00:00' AND '14:00:00'
```

 </details>

 **Задание 11.** Выведите пассажиров с самым длинным ФИО. Пробелы, дефисы и точки считаются частью имени.
<details>
	<summary>Решение</summary>

  ``` sql
SELECT name
FROM Passenger
WHERE LENGTH(name) = (
		SELECT MAX(LENGTH(name))
		FROM Passenger
	)
```

 </details>
 
**Задание 12.** Вывести id и количество пассажиров для всех прошедших полётов
<details>
	<summary>Решение</summary>

  ``` sql
SELECT trip,
	COUNT(*) AS count
FROM Pass_in_trip
GROUP BY trip
```

 </details>

 **Задание 13.** Вывести имена людей, у которых есть полный тёзка среди пассажиров
<details>
	<summary>Решение</summary>

  ``` sql
SELECT name
FROM Passenger
GROUP BY name
HAVING COUNT(*) > 1
```

 </details>

 **Задание 14.** В какие города летал Bruce Willis
<details>
	<summary>Решение</summary>

  ``` sql
SELECT town_to
FROM Trip t
	JOIN Pass_in_trip p ON t.id = p.trip
	JOIN Passenger ON p.passenger = Passenger.id
WHERE Passenger.name = 'Bruce Willis'
```

 </details>

 **Задание 15.** Выведите дату и время прилёта пассажира Стив Мартин (Steve Martin) в Лондон (London)
<details>
	<summary>Решение</summary>

  ``` sql
SELECT time_in
FROM Trip
	JOIN Pass_in_trip ON Trip.id = Pass_in_trip.trip
	JOIN Passenger ON Pass_in_trip.passenger = Passenger.id
WHERE name = 'Steve Martin'
	AND town_to = 'London'
```

 </details>

 **Задание 16.** Вывести отсортированный по количеству перелетов (по убыванию) и имени (по возрастанию) список пассажиров, совершивших хотя бы 1 полет.
<details>
	<summary>Решение</summary>

  ``` sql
SELECT name,
	COUNT(trip) AS count
FROM Passenger
	JOIN Pass_in_trip ON Passenger.id = Pass_in_trip.passenger
GROUP BY Passenger.name
HAVING count(*) >= 1
ORDER BY count DESC,
	name
```

 </details>

 **Задание 17.** Определить, сколько потратил в 2005 году каждый из членов семьи. В результирующей выборке не выводите тех членов семьи, которые ничего не потратили.
<details>
	<summary>Решение</summary>

  ``` sql
SELECT member_name,
	status,
	SUM(amount * unit_price) AS costs
FROM FamilyMembers
	JOIN Payments ON FamilyMembers.member_id = Payments.family_member
WHERE YEAR(date) = 2005
GROUP BY member_name,
	status
```

 </details>

  **Задание 18.** Выведите имя самого старшего человека. Если таких несколько, то выведите их всех.
<details>
	<summary>Решение</summary>

  ``` sql
SELECT member_name
FROM FamilyMembers
WHERE birthday = (
		SELECT MIN(birthday)
		FROM FamilyMembers
	)
```

 </details>

  **Задание 19.** Определить, кто из членов семьи покупал картошку (potato)
<details>
	<summary>Решение</summary>

  ``` sql
SELECT DISTINCT status
FROM FamilyMembers f
	JOIN Payments p ON f.member_id = p.family_member
	JOIN Goods g ON p.good = g.good_id
WHERE good_name = 'potato'
```

 </details>

  **Задание 20.** Сколько и кто из семьи потратил на развлечения (entertainment). Вывести статус в семье, имя, сумму
<details>
	<summary>Решение</summary>

  ``` sql
SELECT status,
	member_name,
	SUM(unit_price * amount) AS costs
FROM FamilyMembers f
	JOIN Payments p ON f.member_id = p.family_member
	JOIN Goods g ON p.good = g.good_id
	JOIN GoodTypes gt ON g.type = gt.good_type_id
GROUP BY status,
	member_name,
	good_type_name
HAVING good_type_name = 'entertainment'
```

 </details>

 
