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
