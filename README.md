# My excercises from sql-ex.ru
## Computer shop
Database scema:
<br/>
![Computer shop](https://sql-ex.ru/images/computers.gif)

## #1
Find the model number, speed, and hard drive size for all PCs under $500. Output: model, speed and hd.
> SELECT model, speed, hd FROM pc WHERE price < 500

## #2
Find printer manufacturers. Output: maker.
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
> <br/> UNION
> <br/> SELECT laptop.model, laptop.price FROM laptop INNER JOIN product ON laptop.model = product.model WHERE product.maker = 'B'
> <br/> UNION
> <br/> SELECT printer.model, printer.price FROM printer INNER JOIN product ON printer.model = product.model WHERE product.maker = 'B'

## #8
Find a PC manufacturer that doesn't produces laptops.
> SELECT DISTINCT maker FROM product WHERE type = 'PC' AND maker NOT IN (SELECT maker FROM product WHERE type = 'Laptop')

## #9
Find PC manufacturers with a processor of at least 450 MHz.
> SELECT DISTINCT maker FROM product WHERE model IN (SELECT model FROM pc WHERE speed >= 450)

## #10
Find the most expensive printer models.
> SELECT model, price FROM printer WHERE price IN (SELECT MAX(price) FROM printer)

## #11
Find the average PC speed.
> SELECT AVG(speed) AS avg_speed FROM pc

## #12
Find the average speed of laptops that cost more than $1,000.
> SELECT AVG(speed) FROM laptop WHERE price > 1000

## #13
Find the average speed of PC manufactured by A.
> SELECT AVG(speed) FROM pc WHERE model IN (SELECT model FROM product WHERE maker = 'A')

## #15
Find hard drive sizes that are the same on two or more PCs. Display: HD
> SELECT hd FROM pc GROUP BY hd HAVING count(hd) > 1


<br></br>
## Ships
Database scema:
<br/>
![Ships](https://sql-ex.ru/images/ships.gif)

## #14
Find the class, name, and country for ships in the Ships table that have at least 10 guns.
> SELECT s.class, s.name, c.country FROM ships s JOIN classes c ON s.class = c.class WHERE numguns >= 10
