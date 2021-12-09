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

## #3
Find the model number, memory size, and screen sizes for notebook PCs priced over $1,000.
> SELECT model, ram, screen FROM laptop WHERE price > 1000

## #4
Find all the entries in the Color Printer table.
> SELECT * FROM printer WHERE color = 'y'

## #5
Find the model number, speed and size of PC hard drives that have 12x or 24x CDs and are priced under $600.
> SELECT model, speed, hd FROM PC WHERE (cd = '12x' OR cd = '24x') AND (price < 600)
