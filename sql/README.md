# SQL learnings

Нужные ссылки:
<a href="https://github.com/mobinni/Complete-SQL-Database-Bootcamp-Zero-to-Mastery/tree/master/SQL%20Deep%20Dive">SQL вопросы на английском</a>

## 1. Select (Выбирать)

Данный запрос используется в случае, если нам нужно показать данные в таблице.

<a href="https://habr.com/ru/post/480838/">В этом ссылке самое основное</a>

#### Tasks (Задании)

<a href="https://www.programiz.com/sql/online-compiler/">Playground (Где можете потренероваться)</a>

1.  Таблица `Customers`. Получить список с информацией обо всех покупателей
    <br>
2.  Таблица `Customers`. Получить список всех клиентов с именем _John_
    <br>
3.  Таблица `Customers`. Получить список всех клиентов с именем _John_ и фамилием _Doe_
    <br>
4.  Таблица `Orders`. Получить список всех заказов с **amount** больше _3_, включая _3_
    <br>
5.  Таблица `Shippings`. Получить список всех посылок с статутом _Pending_
    <br>
6.  Таблица `Orders`. Получить общую сумму всех товаров, переименуйте таблицу на _Все расходы_
    <br>
7.  Таблица `Customers`. Получить список всех клиентов, сортируйте по убывающему списку их возрастов
    <br>
8.  Таблица `Customers`. Получить список имен и фамилий клиентов, другие данные не нужны, сортировка по именам, по возрастающему списку
    <br>
9.  Таблица `Orders`. Получить количество людей купивших _Keyboard_ и _Monitor_
    <br>
10. Таблица `Orders`. Получить список всех заказов у которых сумма находится в промежутке от _300_ до _3000_ (включительно)
    <br>
11. Таблица `Customers`. Получить список количиств людей по странам, в таблице должны быть количество и страны
    <br>
12. Таблица `Customers`. Получить список количиств людей по странам, в таблице должны быть количество и страны, и количества должны быть 2 и больше
    <br>
13. Таблица `Shippings`. Получить количество отправок по статусам, сгруппируте по _Pending_ и _Delivered_, чтобы было видно сколько и какие статусы
    <br>
14. Таблица `Orders`. Получить среднюю значение затрат на вещей
    <br>
15. Таблица `Orders`. Получить список, где **customer_id** сгруппирован на средний чек, и будут показаны те у кого средний чек больше _300_

<a href="https://habr.com/ru/post/461567/">Ссылка на задании</a>

### Агрегатные функции (Aggregate functions)

- `AVG()` - вычисляет среднее значение
- `COUNT()` - подсчитывает строку в указанной таблице или представлении
- `MIN()` - получает минимальное значение
- `MAX()` - получает максимальное значение
- `SUM()` - вычисляет сумму значений

Examples:

```sql
SELECT (emp_no) FROM employess;
```

### Комментировать код (Adding comments)

```sql
-- Простой коммент
-- Второй коммент

/*
Практикуйтесь!
Это коммент, где мы берем сам блок пространство как комент
Хах
*/
```

### Keywords - AND, OR, NOT

- `AND` - сразу две или более условии, где они должны быть верны
- `OR` - сразу две или более условии, где хватает и одной условии
- `NOT` - не равен, то есть меняет с позитивного на отрицательного или наоборот

Examples:

```sql
SELECT firstName, lastName, gender, state FROM customers
WHERE (state = 'OR' OR state = 'NY') AND gender = 'F';

SELECT firstName, gender FROM users
WHERE NOT gender = 'm';

-- Иозраст не равен 55
SELECT age FROM customers
WHERE NOT age = 55;

-- Иозрат не равны 55 и 20
SELECT COUNT(age) FROM customers
WHERE NOT age = 55 AND NOT age =20;
```

### Comparison Operators

```sql
SELECT 10 > 20 -- false
SELECT 10 !> 20 -- true
SELECT 10 !< 20 -- false
SELECT 10 < 20 -- true
SELECT 10 >= 9 -- true
SELECT 10 <= 10 -- true
SELECT 0 = 0 -- true
SELECT 1 != 0 -- true
SELECT 'Mo' = 'mo' --false

```

### Priority chain

По примеру поймите что выйдет с таблицы!

```sql
SELECT * FROM customers
WHERE (
    salary > 10000 AND state = 'NY'
    OR (
        (age > 20 AND age < 30)
        AND salary <= 20000
    )
)
AND gender = 'F';
```

### Empty values (NULL)

- `NULL` - это значить что ничего, то есть его не существует, можете проверить некоторые значении будут показаны как `<NULL>`

```sql
SELECT NULL = NULL; -- null
```

- `IS` - можно использовать с `NULL`, где проверяется существование некоторых элементов

```sql
-- Ввести данные где `state` имеет данные, то есть не NULL
SELECT * FROM customers
WHERE state IS NOT NULL;

-- Ввести данные где `state` не имеет данные, то есть NULL
SELECT * FROM customers
WHERE state IS NULL;

SELECT * FROM users
WHERE age = 20 IS FALSE;
-- РАвна
SELECT * FROM users
WHERE age != 20;
```

- `coalesce` - заменяет `NULL` на то что будет указано, например, внизу написали 'Empty' если столбцы пусты

```sql
-- Структура
SELECT coalesce(
    <column1>,
    <column2>,
    <column3>,
    'Empty'
    ) AS combined_columns FROM <table>
```

```sql
-- В данным случае мы заменяем пустые значении в `age` на 20, можно использовать другие значения
SELECT sum(coalesce(age, 20)) FROM customers
```

#### Keywords - BETWEEN AND

- `BETWEEN AND` - между какиеми то отрезками, используются с числами

```sql
SELECT <column> FROM  <table>
WHERE <column> BETWEEN X AND Y
```

```sql
SELECT * FROM customers
WHERE age BETWEEN 20 AND 40
-- Они равны
SELECT * FROM customers
WHERE age >= 20 AND age <= 40
```

#### Keywords - IN
