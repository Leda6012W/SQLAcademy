### SQLAcademy
Решения задач из тренажёра [SQL Academy](sql-academy.org).

**Задание 1.** Вывести имена всех людей, которые есть в базе данных авиакомпаний

<details>
	<summary>Решение</summary>
`SELECT name
FROM Passenger`
</details>

**Задание 2.** Вывести названия всеx авиакомпаний
<details>
	<summary>Решение</summary>
SELECT name
FROM Company
</details>

**Задание 3.** Вывести все рейсы, совершенные из Москвы
<details>
	<summary>Решение</summary>
SELECT *
FROM Trip
WHERE town_from = 'Moscow';
</details>

**Задание 4.** Вывести имена людей, которые заканчиваются на "man"
<details>
	<summary>Решение</summary>
SELECT name
FROM Passenger
WHERE name LIKE '%man'
</details>

**Задание 5.** Вывести количество рейсов, совершенных на TU-134
<details>
	<summary>Решение</summary>
SELECT COUNT(*) as count
FROM Trip
WHERE plane = 'TU-134'
</details>

**Задание 6.** Какие компании совершали перелеты на Boeing
<details>
	<summary>Решение</summary>
SELECT DISTINCT name
FROM Trip
	JOIN Company on Trip.company = Company.id
WHERE plane = 'Boeing';
</details>

**Задание 7.** Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)
<details>
	<summary>Решение</summary>
SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'
</details>

**Задание 8.** В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?
<details>
	<summary>Решение</summary>
SELECT town_to,
	TIMEDIFF(time_in, time_out) as flight_time
from Trip
WHERE town_from = 'Paris'
</details>

**Задание 9.** Какие компании организуют перелеты из Владивостока (Vladivostok)?
<details>
	<summary>Решение</summary>
SELECT Company.name
from Trip
	INNER JOIN Company on Trip.company = Company.id
WHERE town_from = 'Vladivostok'
</details>

**Задание 10.** Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.
<details>
	<summary>Решение</summary>
SELECT *
FROM Trip
WHERE DATE(time_out) = '1900-01-01'
	AND TIME(time_out) BETWEEN '10:00:00' AND '14:00:00'
 </details>
 
