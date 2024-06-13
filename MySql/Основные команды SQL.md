## Настройка базы данных

Перед началом создайте БД с тестовыми данными. Для работы вам понадобится скачать два файла: [DLL.sql](https://drive.google.com/file/d/0B_oq3-doZhC-ME1lUlR3a3pYRU0/view?resourcekey=0-flfPMq0i6E6-i5BX27Se4g) и [InsertStatements.sql](https://drive.google.com/file/d/0B_oq3-doZhC-TV9ud1JubkVDaXM/view?resourcekey=0-CToHONw06G5QQ6DuRf68Ng). После установите MySQL, откройте терминал и войдите в консоль MySQL с помощью команды:

```
mysql -u root -p
```

Затем введите пароль и выполните следующую команду. Назовём базу данных «university»:

```
CREATE DATABASE university;
USE university;
SOURCE <path_of_DLL.sql_file>;
SOURCE <path_of_InsertStatements.sql_file>;
```

## SHOW DATABASES

SQL-команда, которая отвечает за просмотр доступных баз данных.

## CREATE DATABASE

Команда для создания новой базы данных.

## USE

С помощью этой SQL-команды `USE <database_name>` выбирается база данных, необходимая для дальнейшей работы с ней.

## SOURCE

А `SOURCE <file.sql>` позволит выполнить сразу несколько SQL-команд, содержащихся в файле с расширением .sql.

## DROP DATABASE

Стандартная SQL-команда для удаления целой базы данных.

## SHOW TABLES

С помощью этой несложной команды можно увидеть все таблицы, которые доступны в базе данных.

## CREATE TABLE

SQL-команда для создания новой таблицы:

```
CREATE TABLE <table_name1> (
  <col_name1><col_type1>,
  <col_name2><col_type2>,
  <col_name3><col_type3>
  PRIMARY KEY(<col_name1>),
  FOREIGN KEY(<col_name2>) REFERENCES <table_name2>(<col_name2>)
);
```

#### Ограничения целостности при использовании CREATE TABLE

Может понадобиться создать ограничения для определённых столбцов в таблице. При создании таблицы можно задать следующие ограничения:

- ячейка таблицы не может иметь значение `NULL`;
- первичный ключ — `PRIMARY KEY(col_name1, col_name2, …)`;
- внешний ключ — `FOREIGN KEY(col_namex1, …, col_namexn) REFERENCES table_name(col_namex1, …, col_namexn)`.

Можно задать больше одного первичного ключа. В этом случае получится составной первичный ключ.

#### Пример

Создайте таблицу «instructor»:

```
CREATE TABLE instructor (
  ID CHAR(5),
  name VARCHAR(20) NOT NULL,
  dept_name VARCHAR(20),
  salary NUMERIC(8,2),
  PRIMARY KEY (ID),
  FOREIGN KEY (dept_name) REFERENCES department(dept_name)
);
```

## DESCRIBE

С помощью `DESCRIBE <table_name>` можно просмотреть различные сведения (тип значений, является ключом или нет) о столбцах таблицы.

## INSERT

Команда `INSERT INTO <table_name>` в SQL отвечает за добавление данных в таблицу:

```
INSERT INTO <table_name> (<col_name1>, <col_name2>, <col_name3>, …)
  VALUES (<value1>, <value2>, <value3>, …);
```

При добавлении данных в каждый столбец таблицы не требуется указывать названия столбцов.

```
INSERT INTO <table_name>
  VALUES (<value1>, <value2>, <value3>, …);
```

## UPDATE

SQL-команда для обновления данных таблицы:

```
UPDATE <table_name>
  SET <col_name1> = <value1>, <col_name2> = <value2>, ...
  WHERE <condition>;
```

## DELETE

SQL-команда `DELETE FROM <table_name>` используется для удаления данных из таблицы.

## DROP TABLE

А так можно удалить всю таблицу целиком.

## SELECT

Далее мы рассмотрим основные команды SQL, которые позволяют работать непосредственно с данными. К одной из таких SQL-команд относится `SELECT` для получения данных из выбранной таблицы:

```
SELECT <col_name1>, <col_name2>, …
  FROM <table_name>;
```

Следующей командой можно вывести все данные из таблицы:

```
SELECT * FROM <table_name>;
```

## SELECT DISTINCT

В столбцах таблицы могут содержаться повторяющиеся данные. Используйте `SELECT DISTINCT` для получения только неповторяющихся данных.

```
SELECT DISTINCT <col_name1>, <col_name2>, …
  FROM <table_name>;
```

## WHERE

Можно использовать ключевое слово `WHERE` в `SELECT` для указания условий в запросе:

```
SELECT <col_name1>, <col_name2>, …
  FROM <table_name>
  WHERE <condition>;
```

В запросе можно задавать следующие условия:

- сравнение текста;
- сравнение численных значений;
- логические операции `AND` (и), `OR` (или) и `NOT` (отрицание).

#### Пример

Попробуйте выполнить следующие команды. Обратите внимание на условия, заданные в `WHERE`:

```
SELECT * FROM course WHERE dept_name=’Comp. Sci.’;
SELECT * FROM course WHERE credits>3;
SELECT * FROM course WHERE dept_name='Comp. Sci.' AND credits>3;
```

![Основные команды SQL, которые должен знать каждый программист 1](https://media.tproger.ru/uploads/2018/09/6.png)

SQL-команды: пример вывода с WHERE

## GROUP BY

Оператор `GROUP BY` часто используется с агрегатными функциями, такими как `COUNT`, `MAX`, `MIN`, `SUM` и `AVG`, для группировки выходных значений.

```
SELECT <col_name1>, <col_name2>, …
  FROM <table_name>
  GROUP BY <col_namex>;
```

#### Пример

Выведем количество курсов для каждого факультета:

```
SELECT COUNT(course_id), dept_name
  FROM course
  GROUP BY dept_name;
```

![Основные команды SQL, которые должен знать каждый программист 2](https://media.tproger.ru/uploads/2018/09/7.png)

SQL-команды: пример вывода с GROUP BY

## HAVING

Ключевое слово `HAVING` было добавлено в SQL по той причине, что `WHERE` не может использоваться для работы с агрегатными функциями.

```
SELECT <col_name1>, <col_name2>, ...
  FROM <table_name>
  GROUP BY <column_namex>
  HAVING <condition>
```

#### Пример

Выведем список факультетов, у которых более одного курса:

```
SELECT COUNT(course_id), dept_name
  FROM course
  GROUP BY dept_name
  HAVING COUNT(course_id)>1;
```

![Основные команды SQL, которые должен знать каждый программист 3](https://media.tproger.ru/uploads/2018/09/8.png)

SQL-команды: пример вывода с HAVING

## ORDER BY

`ORDER BY` используется для сортировки результатов запроса по убыванию или возрастанию. `ORDER BY` отсортирует по возрастанию, если не будет указан способ сортировки `ASC` или `DESC`.

```
SELECT <col_name1>, <col_name2>, …
  FROM <table_name>
  ORDER BY <col_name1>, <col_name2>, … ASC|DESC;
```

#### Пример

Выведем список курсов по возрастанию и убыванию количества кредитов:

```
SELECT * FROM course ORDER BY credits;
SELECT * FROM course ORDER BY credits DESC;
```

## BETWEEN

`BETWEEN` используется для выбора значений данных из определённого промежутка. Могут быть использованы числовые и текстовые значения, а также даты.

```
SELECT <col_name1>, <col_name2>, …
  FROM <table_name>
  WHERE <col_namex> BETWEEN <value1> AND <value2>;
```

#### Пример

Выведем список инструкторов, чья зарплата больше 50 000, но меньше 100 000:

```
SELECT * FROM instructor
  WHERE salary BETWEEN 50000 AND 100000;
```

## LIKE

Оператор `LIKE` используется в `WHERE`, чтобы задать шаблон поиска похожего значения.

Есть два свободных оператора, которые используются в `LIKE`:

- `%` (ни одного, один или несколько символов);
- `_` (один символ).

```
SELECT <col_name1>, <col_name2>, …
  FROM <table_name>
  WHERE <col_namex> LIKE <pattern>;
```

#### Пример

Выведем список курсов, в имени которых содержится `«to»`, и список курсов, название которых начинается с `«CS-»`:

```
SELECT * FROM course WHERE title LIKE ‘%to%’;
SELECT * FROM course WHERE course_id LIKE 'CS-___';
```

![Основные команды SQL, которые должен знать каждый программист 4](https://media.tproger.ru/uploads/2018/09/11.png)

SQL-команды: пример вывода с LIKE

## IN

С помощью `IN` можно указать несколько значений для оператора `WHERE`:

```
SELECT <col_name1>, <col_name2>, …
  FROM <table_name>
  WHERE <col_namen> IN (<value1>, <value2>, …);
```

#### Пример

Выведем список студентов с направлений Comp. Sci., Physics и Elec. Eng.:

```
SELECT * FROM student
  WHERE dept_name IN (‘Comp. Sci.’, ‘Physics’, ‘Elec. Eng.’);
```

## JOIN

`JOIN` используется для связи двух или более таблиц с помощью общих атрибутов внутри них. На изображении ниже показаны различные способы объединения в SQL. Обратите внимание на разницу между левым внешним объединением и правым внешним объединением:

![Основные команды SQL, которые должен знать каждый программист 5](https://media.tproger.ru/uploads/2018/09/13.jpg)

SQL-команды: схема использования JOIN

```
SELECT <col_name1>, <col_name2>, …
  FROM <table_name1>
  JOIN <table_name2>
  ON <table_name1.col_namex> = <table2.col_namex>;
```

#### Пример

Выведем список всех обязательных курсов и детали о них:

```
SELECT prereq.course_id, title, dept_name, credits, prereq_id
  FROM prereq
  LEFT OUTER JOIN course
  ON prereq.course_id=course.course_id;
```

![Основные команды SQL, которые должен знать каждый программист 6](https://media.tproger.ru/uploads/2018/09/15.png)

SQL-команды: пример вывода с JOIN

## VIEW

`VIEW` — это виртуальная таблица SQL, созданная в результате выполнения выражения. Она содержит строки и столбцы и очень похожа на обычную SQL-таблицу. `VIEW` всегда показывает самую свежую информацию из базы данных.

#### Создание

```
CREATE VIEW <view_name> AS
  SELECT <col_name1>, <col_name2>, …
  FROM <table_name>
  WHERE <condition>;
```

#### Удаление

```
DROP VIEW <view_name>;
```

## Агрегатные функции

Это не совсем основные команды SQL, однако знать их тоже желательно. Агрегатные функции используются для получения совокупного результата, относящегося к рассматриваемым данным:

- `COUNT(col_name)` — возвращает количество строк;
- `SUM(col_name)` — возвращает сумму значений в данном столбце;
- `AVG(col_name)` — возвращает среднее значение данного столбца;
- `MIN(col_name)` — возвращает наименьшее значение данного столбца;
- `MAX(col_name)` — возвращает наибольшее значение данного столбца.

## Вложенные подзапросы

Вложенные подзапросы — это SQL-запросы, которые включают выражения `SELECT`, `FROM` и `WHERE`, вложенные в другой запрос.

#### Пример

Найдём курсы, которые преподавались осенью 2009 и весной 2010 годов:

```
SELECT DISTINCT course_id
  FROM section
  WHERE semester = ‘Fall’ AND year= 2009 AND course_id IN (
    SELECT course_id
    FROM section
    WHERE semester = ‘Spring’ AND year= 2010
  );
```