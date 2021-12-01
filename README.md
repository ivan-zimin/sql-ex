# My excercises from sql-ex.ru
## Computer shop
Database scema:
<br />
![Computer shop](https://sql-ex.ru/images/computers.gif)

## #1
Find the model number, speed, and hard drive size for all PCs under $500. Output: model, speed and hd
> SELECT model, speed, hd FROM pc WHERE price < 500

## #2
Find printer manufacturers. Output: maker
> SELECT DISTINCT maker FROM product WHERE type = 'Printer'
