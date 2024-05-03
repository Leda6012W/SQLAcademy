### SQLAcademy
Решения задач из тренажёра [SQL Academy](sql-academy.org).
**Задание 1.** Вывести имена всех людей, которые есть в базе данных авиакомпаний

<details>
  <summary>Решение</summary>
  SELECT name
FROM Passenger
</details>

**Задание 2.** Вывести названия всеx авиакомпаний

SELECT name
FROM Company

**Задание 3.** Вывести все рейсы, совершенные из Москвы

SELECT *
FROM Trip
WHERE town_from = 'Moscow';

**Задание 4.** Вывести имена людей, которые заканчиваются на "man"

SELECT name
FROM Passenger
WHERE name LIKE '%man'

**Задание 5.** Вывести количество рейсов, совершенных на TU-134

SELECT COUNT(*) as count
FROM Trip
WHERE plane = 'TU-134'

**Задание 6.** Какие компании совершали перелеты на Boeing

SELECT DISTINCT name
FROM Trip
	JOIN Company on Trip.company = Company.id
WHERE plane = 'Boeing';

**Задание 7.** Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)

SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'

**Задание 8.** В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?

SELECT town_to,
	TIMEDIFF(time_in, time_out) as flight_time
from Trip
WHERE town_from = 'Paris'

**Задание 9.** Какие компании организуют перелеты из Владивостока (Vladivostok)?

SELECT Company.name
from Trip
	INNER JOIN Company on Trip.company = Company.id
WHERE town_from = 'Vladivostok'

**Задание 10.** Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.

SELECT *
FROM Trip
WHERE DATE(time_out) = '1900-01-01'
	AND TIME(time_out) BETWEEN '10:00:00' AND '14:00:00'
