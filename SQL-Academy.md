**Что такое встроенная функция**

13.34 - 14.34 SQL
Встроенная функция – реализованный в СУБД кусок кода, с помощью которого можно выполнять преобразования строковых, числовых и других данных в запросах.

Каждая функция принимает набор аргументов определённого типа, выполняет заложенные в неё операции и обязательно возвращает один из возможных литералов. Стоит отметить, что функции могут принимать как ноль аргументов, так и несколько.

Например, функция NOW() принимает ноль аргументов и возвращает литерал в формате даты, а LENGTH('sql-academy') принимает один строковый аргумент и возвращает числовой литерал «11».

*Instr*
Поиск подстроки в строке
```sql
SELECT INSTR('sql-academy', 'academy') AS idx;
```


Выведите текст "Hello world" в нижнем регистре с помощью соответствующей функции.
```sql
SELECT LOWER('SQL Academy') AS lower_string;
```


YEAR 
Возвращает год для указанной даты
```sql
SELECT YEAR("2022-06-16") AS year;
```


SELECT YEAR("1960-05-13T00:00:00.000Z") AS year;

```sql
SELECT member_name,
	YEAR(birthday) AS year_of_birth
FROM FamilyMembers;
```

Выведите полное имя члена семьи и длину его фамилии.

---

Для вывода длины фамилии используйте псевдоним lastname_length.

```sql
SELECT member_name,
	LENGTH(member_name) - INSTR(member_name, ' ') AS lastname_length
FROM FamilyMembers;
```


**Исключение дубликатов, DISTINCT**

 Выведем поле class из таблицы Student_in_class из базы данных, в которой организовано хранение информации о расписании занятий в школе.
```sql
SELECT class FROM Student_in_class;
```
Оператор DISTINCT
Чтобы при выборке исключить повторяющиеся результаты
```sql
SELECT DISTINCT class FROM Student_in_class;
```

```sql
SELECT DISTINCT first_name, last_name FROM User;
```

```sql
SELECT DISTINCT teacher, subject FROM Schedule;
```


**Условный оператор WHERE**

```sql
SELECT * FROM Student
WHERE first_name = "Grigorij" AND YEAR(birthday) > 2000;
```
## [Операторы сравнения](https://sql-academy.org/ru/guide/conditional-where-operator#operatory-sravneniya)

Операторы сравнения служат для сравнения 2 выражений, результатом которого может являться:

- true (что эквивалентно 1)
- false (что эквивалентно 0)
- NULL

| Оператор         | Обозначение | Описание                                                                                                                                                         |
| :--------------- | :---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Равенство        | =           | Если оба значения равны, то результат будет равен 1, иначе 0                                                                                                     |
| Эквивалентность  | <=>         | Аналогичен оператору равенства, за исключением того, что результат будет равен 1 в случае сравнения NULL с NULL и 0, когда идёт сравнение любого значения с NULL |
| Неравенство      | <> или !=   | Если оба значения не равны, то результат будет равен 1, иначе 0                                                                                                  |
| Меньше           | <           | Если одно значение меньше другого, то результат будет равен 1, иначе 0                                                                                           |
| Меньше или равно | <=          | Если одно значение меньше или равно другому, то результат будет равен 1, иначе 0                                                                                 |
| Больше           | >           | Если одно значение больше другого, то результат будет равен 1, иначе 0                                                                                           |
| Больше или равно | >=          | Если одно значение больше или равно другому, то результат будет равен 1, иначе 0                                                                                 |
## [Логические операторы](https://sql-academy.org/ru/guide/conditional-where-operator#logicheskie-operatory)

Логические операторы необходимы для связывания операторов сравнения.

|Оператор|Описание|
|:--|:--|
|NOT|Меняет значение оператора сравнения на противоположный|
|OR|Возвращает общее значение выражения истинно, если хотя бы одно из них истинно|
|AND|Возвращает общее значение выражения истинно, если они оба истинны|
|XOR|Возвращает общее значение выражения истинно, если один и только один аргумент является истинным|

Давайте для примера выведем все полёты, которые были совершены на самолёте «Boeing», но, при этом, вылет был не из Лондона:

MySQL

```sql
SELECT * FROM Trip
WHERE plane = 'Boeing' AND NOT town_from = 'London';
```

```sql
SELECT good FROM Payments WHERE unit_price > 2000;
```


```sql
SELECT member_name FROM FamilyMembers WHERE status = "father";
```

```sql
SELECT member_name,birthday FROM FamilyMembers WHERE status= "father" OR  status="mother";
```

```sql
SELECT *  FROM Rooms WHERE has_kitchen = true AND has_internet = true;
```

**IS NULL**

Оператор IS NULL позволяет узнать равно ли проверяемое значение NULL, т.е. пустое ли значение

```sql
SELECT * FROM Teacher
WHERE middle_name IS NULL;
```

```sql
SELECT * FROM Teacher
WHERE middle_name IS NOT NULL;
```

**BETWEEN**

Оператор BETWEEN min AND max позволяет узнать расположено ли проверяемое значение столбца в интервале между min и max, включая сами значения min и max

```sql
SELECT * FROM Payments
WHERE unit_price BETWEEN 100 AND 500;
```

**IN**
Оператор IN позволяет узнать входит ли проверяемое значение столбца в список определённых значений.
```sql
SELECT * FROM FamilyMembers
WHERE status IN ('father', 'mother');
```

```sql
SELECT first_name,last_name FROM Student WHERE middle_name IS NULL;
```

```sql
SELECT room_id, start_date, end_date FROM Reservations WHERE total BETWEEN 500 AND 1200;
```
Выведите информацию о студентах из таблицы Student, у которых год рождения соответствует одному из перечисленных: 2000, 2002 и 2004.
```sql
SELECT * FROM Student WHERE YEAR(birthday) IN (2000,2002,2004);
```