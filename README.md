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

## #16
Find pairs of PC models that have the same speed and RAM. On the output, each pair should be shown only once, i.e. (i,j) but not (j,i), Output order: higher model, lower model, speed, and RAM.
> SELECT DISTINCT a.model, b.model, a.speed, a.ram
> FROM pc a, pc b
> WHERE a.speed = b.speed AND a.ram = b.ram AND a.model > b.model

## #17
Find laptop models that are slower than the speed of each of the PCs.
Output: type, model, speed
> SELECT DISTINCT product.type, product.model, laptop.speed
FROM laptop
JOIN product ON laptop.model = product.model
WHERE laptop.speed < (SELECT MIN(speed) FROM pc)

## #18
Find manufacturers of the cheapest color printers. Output: maker, price.
> SELECT DISTINCT maker, price FROM product JOIN printer ON product.model = printer.model WHERE color = 'y' AND price = (SELECT MIN(price) FROM printer WHERE color = 'y')

## #19
For each manufacturer that has models in the Laptop table, find the average screen size of their notebook PCs.
Output: maker, average screen size.
> SELECT p.maker, AVG(l.screen) FROM product p
INNER JOIN laptop l ON p.model = l.model
GROUP BY p.maker

## #20
Find manufacturers that make at least three different PC models. Output: Maker, number of PC models.
> SELECT maker, COUNT(1)
FROM product
WHERE type = 'pc'
GROUP BY maker
HAVING COUNT(1) >= 3

## #21
Find the maximum price of PCs produced by each manufacturer that has models in the PC table. Output: maker, maximum price.
> SELECT maker, MAX(price) FROM product
INNER JOIN pc ON product.model = pc.model
GROUP BY maker

## #22
For each PC speed that exceeds 600 MHz, determine the average price of a PC with the same speed. Output: speed, average price.
> SELECT speed, AVG(price) FROM pc
WHERE speed > 600
GROUP BY speed

## #23
Find manufacturers that produce PCs with a speed of at least 750 MHz and PC laptops with a speed of at least 750 MHz.
Display: Maker
> SELECT DISTINCT maker
FROM product
INNER JOIN pc ON product.model = pc.model
WHERE speed >= 750
AND maker IN
(SELECT maker
FROM product
INNER JOIN laptop ON product.model = laptop.model
WHERE speed >= 750)

## #24
List the model numbers of any type that have the highest price of all the products in the database.
> SELECT model FROM (
SELECT model, price FROM pc
UNION
SELECT model, price FROM laptop
UNION
SELECT model, price FROM printer
) t1 WHERE price = (
SELECT MAX(price) FROM (
SELECT model, price FROM pc
UNION
SELECT model, price FROM laptop
UNION
SELECT model, price FROM printer
) t2
)

<br></br>
## Ships
Database scema:
<br/>
![Ships](https://sql-ex.ru/images/ships.gif)

## #14
Find the class, name, and country for ships in the Ships table that have at least 10 guns.
> SELECT s.class, s.name, c.country FROM ships s JOIN classes c ON s.class = c.class WHERE numguns >= 10

## #31
Find classes of ships whose guns are at least 16 inches in bore. Output: class and country.
> SELECT class, country FROM Classes WHERE bore >=16

## #33
List the ships sunk in battles in the North Atlantic. Output: ship.
> SELECT ship FROM outcomes
INNER JOIN battles ON outcomes.battle = battles.name
WHERE result = 'sunk' AND battles.name = 'North Atlantic'
