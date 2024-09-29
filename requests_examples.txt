Create table book:
CREATE TABLE book (
    book_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(50),
    author VARCHAR(30),
    price DECIMAL(8 , 2 ),
    amount INT
);

Add new rows: 
INSERT INTO book (title, author, price, amount)
VALUES  
('Мастер и Маргарита', 'Булгаков М.А.', '670.99', '3'),
('Белая гвардия', 'Булгаков М.А.', '540.50', '5'),
('Идиот', 'Достоевский Ф.М.', '460.00', '10'),
('Братья Карамазовы', 'Достоевский Ф.М.', '799.01', '2')
;

Select data from table:
SELECT * from book;
or 
SELECT title, amount  FROM book;

Delete row:
DELETE FROM book WHERE book_id=3;

Обновить book_id, чтобы шло 1,2,3,4, а не 1,3,4,5:
-- Удалите старый столбец book_id
ALTER TABLE book DROP COLUMN book_id;

-- Добавьте новый столбец book_id с AUTO_INCREMENT
ALTER TABLE book ADD COLUMN book_id INT PRIMARY KEY AUTO_INCREMENT FIRST;

Check that new row will be added without any errors:
INSERT INTO book (title, author, price, amount) VALUES 
('Новое название', 'Новый автор', 100.00, 1);
SELECT * FROM book;

Пример кругления:
SELECT title, author, amount, ROUND((price*0.7),2) AS new_price
FROM book;

Example with IF:
SELECT author, title, 
ROUND(IF (author = 'Булгаков М.А.', price*1.1, IF(author = 'Есенин С.А.', price*1.05, price)),2) as new_price
FROM book;

Example with WHERE:
SELECT title, author, price, amount FROM book
WHERE (price<500 or price>600) AND amount * price>=5000;

Example with BETWEEN and IN:
SELECT title, author FROM book
WHERE (price BETWEEN 540.50 AND 800) AND amount IN(2,3,5,7);

Example of sorting: ASC - в алфавитном порядке, DESC- наоборот
SELECT author, title FROM book
WHERE (amount BETWEEN 2 AND 14)
ORDER BY author DESC, title ASC;