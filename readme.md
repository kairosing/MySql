MySql

Краткий урок по базе данных

Чтобы зайти в mysql через docker контейнер надо прописать в терминале mysql -P 33061 --protocol=tcp -u root -p
попросит пароль.

Для того чтобы посмотреть созданные базы данных прописываем
SHOW DATABASES;
после каждого скрипта надо ставить точку с запятой.

Чтобы создать новую базу данных пишем скрипт
CREATE DATABASE имя базы например sql_course

Теперь удаляем DROP DATABASE sql_course;

Для того чтобы использовать какую ту конкретную БД прописываем USE sql_course;

Что бы посмотреть таблицы в этой БД прописываем show tables;

создаем первую таблицу CREATE TABLE teacher(
-> id INT AUTO_INCREMENT PRIMARY KEY,
-> surname VARCHAR(255) NOT NULL
-> );


Что бы посмотреть какие поля созданы в этой таблицы
show columns FROM teacher;

Теперь я создам еще одну БД
CREATE TABLE lesson(
-> id INT AUTO_INCREMENT PRIMARY KEY,
-> name VARCHAR(255) NOT NULL,
-> teacher_id INT NOT NULL,
-> FOREIGN KEY (teacher_id) references teacher(id)
-> );

Теперь я сделал 2 таблицы связанные между собой

show tables;

Для того чтобы вставить новую запись в таблицу
INSERT INTO teacher (surname) values ("Иванов");

Для того чтобы посмотреть таблицу
SELECT * FROM teacher;
SELECT id FROM teacher;
Их можно даже дублировать
SELECT id, surname, surname FROM teacher;

SELECT DISTINCT surname FROM teacher;
тут мы видим что имя встречается единожды 

так же можно выводить
SELECT * FROM teacher WHERE id = 1;
SELECT * FROM teacher WHERE id = 3;
SELECT * FROM teacher WHERE id > 3;
SELECT * FROM teacher WHERE id < 3;
SELECT * FROM teacher WHERE surname = "Петров";
SELECT * FROM teacher WHERE surname = "Петров" LIMIT 2;
SELECT * FROM teacher LIMIT 2;

Так же можно заменить
SELECT id AS 'Идентификатор', surname AS 'Фамилия' FROM teacher;

Если хотим отсортировать по id
SELECT * FROM teacher ORDER BY id;

если в обратном порядке
SELECT * FROM teacher ORDER BY id DESC;


Добавим еще одно поля в таблицу с помощью ALTER
ALTER TABLE teacher ADD age INT;

теперь смотрим добавил
show columns from teacher;

Для обновление данных в таблице UPDATE
UPDATE teacher SET age = 20 where id=1;


При задание условия можем поставить LIKE после него задается определенный шаблон
SELECT * FROM teacher WHERE surname LIKE "%ов"
так он всех выведит на концовке %ов
SELECT * FROM teacher WHERE surname LIKE "%ин";
теперь выведит на концовке ин
SELECT * FROM teacher WHERE surname LIKE "п%ов";

Логические операторы where and or
SELECT * FROM teacher WHERE id > 3 AND age < 45;
SELECT * FROM teacher WHERE id > 4 OR age < 31;
SELECT * FROM teacher WHERE NOT id = 2;

Для того чтобы получить выборку между двумя значениями используется BETWEEN
SELECT * FROM teacher WHERE age BETWEEN 35 and 45;

Для того что бы удолить DELETE
DELETE FROM teacher WHERE id = 6;





INNER JOIN, LEFT JOIN, RIGHT JOIN

mysql> select * from teacher;

id  surname    age     

1  Иванов     20  

2  Петров     25 

3  Сидоров    30 

4  Петров     35 

5  Чижкин     40 



id  name  teacher_id 

1  Математика  1 

2  Информатика 1 

3  Русский     2

4  Физика      3 


Есть 2 таблицы teacher OR lesson

mysql> SELECT teacher.surname, lesson.name FROM teacher INNER JOIN lesson ON teacher.id = lesson.teacher_id;
ВЫБЕРИТЕ имя учителя, имя урока ОТ учителя ВНУТРЕННИЕ ПРИСОЕДИНЯЙТЕСЬ к уроку НА учителе. id = урок. учитель _id;

surname      name  

Иванов     Математика

Иванов     Информатика

Петров     Русский

Сидоров    Физика



mysql> mysql> SELECT teacher.surname, lesson.name FROM teacher LEFT OUTER JOIN lesson ON teacher.id = lesson.teacher_i

surname   name  

Иванов    Математика

Иванов    Информатика

Петров    Русский

Сидоров   Физика

Петров    NULL

Чижкин    NULL



mysql> mysql> SELECT teacher.surname, lesson.name FROM teacher RIGHT OUTER JOIN lesson ON teacher.id = lesson.teacher_

surname      name  

Иванов       Математика

Иванов       Информатика

Петров       Русский

Сидоров      Физика



mysql> SELECT * FROM teacher UNION SELECT * FROM lesson;

id  surname    age

1   Иванов    20 

2   Петров    25 

3   Сидоров   30 

4   Петров    35 

5   Чижкин    40 

1   Математика   1 

2   Информатика  1 

3   Русский      2 

4   Физика       3 


Функция возврашает средний возвраст
mysql> SELECT AVG(age) FROM teacher;

AVG(age) 

30.0000 



SELECT MAX(age), MIN(age)  FROM teacher;

MAX(age)  MIN(age) 

       40        20 



mysql> SELECT SUM(age) FROM teacher;

 SUM(age) 

     150 



SELECT age, COUNT(age) FROM teacher GROUP BY age;

age   COUNT(age) 

  20           1 

  25           2 

  30           2

  35           1 

  40           1 

