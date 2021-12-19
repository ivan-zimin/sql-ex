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

## #6
Find the speeds of such notebooks for each manufacturer that produces notebook PCs with a hard disk volume of at least 10 GB. Output: manufacturer, speed.
> SELECT DISTINCT product.maker AS Maker, laptop.speed AS speed FROM product INNER JOIN laptop ON product.model = laptop.model WHERE laptop.hd >= 10

## #7
Find the model numbers and prices of all vendors selling products (of any type) from maker B.
> SELECT pc.model, pc.price FROM pc INNER JOIN product ON pc.model = product.model WHERE product.maker = 'B'
> <br /> UNION
> <br /> SELECT laptop.model, laptop.price FROM laptop INNER JOIN product ON laptop.model = product.model WHERE product.maker = 'B'
> <br /> UNION
> <br /> SELECT printer.model, printer.price FROM printer INNER JOIN product ON printer.model = product.model WHERE product.maker = 'B'