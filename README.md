-- 1.1
SELECT CustomerID, CompanyName, Address
FROM Customers
WHERE City =  'London' OR City = 'Paris'
/*The code is self explanitory, but I just got the columns needed for the question,
the table where I wanted it from which was Customers and then I gave it a condition to
display only the values where the city is either London or Paris*/

-- 1.2
SELECT ProductName
FROM Products
WHERE  (QuantityPerUnit LIKE '%bottles%')
/*I selected the column of ProductName from the Products table, then I added a condition
where it would only show me products from each row that have the word"bottles" in them*/

-- 1.3
SELECT c.ProductName, s.CompanyName, s.Country
FROM Products c
    INNER JOIN Suppliers s ON c.SupplierID = s.SupplierID
WHERE  (QuantityPerUnit LIKE '%bottles%')
/*Here, I done the same as 1.2, but I added another statement which joined another table.
That table was suppliers. You can see this after "INNER JOIN" the c and s is just an alias
given to the table names. This was just to save time when writing the code*/

-- 1.4
SELECT SUM(c.CategoryID), c.CategoryName
FROM Categories c
    INNER JOIN Products p ON c.CategoryID = p.CategoryID
        GROUP BY CategoryName
        ORDER BY SUM(c.CategoryID) DESC
/*I used the SUM function here for the category so that I could add up all the products with that key
I then joined the Products table so that I could get the names and total amounts to join each other
and used DESC to display the highest to lowest numbers*/

-- 1.5
SELECT CONCAT(TitleOfCourtesy, FirstName, ' ', LastName) AS 'Name & Title', City
FROM Employees WHERE Country LIKE '%UK%'
/*The question said I have to concatenate, so I put together three different columns into one.
They were the ones you see in the brackets. The empty quotes just puts a space between the first
and last name. Finally, I put a rule in the WHERE function that these people can only be from the UK*/

-- 1.6
SELECT r.RegionID, ROUND (SUM(od.UnitPrice * od.Quantity * 1-Discount),0) AS "Sales Total"
FROM Territories t
    INNER JOIN Region r ON t.RegionID = r.RegionID
    INNER JOIN EmployeeTerritories et ON et.TerritoryID = t.TerritoryID
    INNER JOIN Orders o ON et.EmployeeID = o.EmployeeID
    INNER JOIN [Order Details] od ON o.OrderID = od.OrderID
        GROUP BY r.RegionID
        ORDER BY ROUND (SUM(od.UnitPrice * od.Quantity * 1-Discount),0)
/*I partly completed this because I only did the first part of what the question wanted me to do.
I connected 5 tables which had one key linking to another together in order to find the sales totals
for all sales regions. I couldn't do the part of it being higher than a million, but I did round
to present the final answer*/

-- 1.7
SELECT COUNT(Freight) AS "Freight Count"
FROM Orders
WHERE Freight > 100.00 AND ShipCountry = 'USA' OR ShipCountry = 'UK'
/*Here I just counted from the orders table from where the country shipped to was either UK or USA
and used the WHERE function to show only those above 100.00*/

-- 1.8
SELECT TOP 1 OrderID, UnitPrice * Quantity * Discount AS "Highest Item"
FROM [Order Details]
GROUP BY OrderID, (UnitPrice * Quantity * Discount)
HAVING (UnitPrice * Quantity * Discount) = (SELECT MAX (UnitPrice * Quantity * Discount) FROM [Order Details])
ORDER BY MAX(UnitPrice * Quantity * Discount)
/*I used my code here to find only the first order with the highest number of discount applied, hence the "TOP 1"
The rest is self explanitory but it was just some mathematical orders to properly calculate the discount.*/

-- 2.1
CREATE DATABASE StudentInfo
CREATE TABLE Sparta (
    ID int identity (1,1),
    Title varchar(255),
    FirstName varchar(255),
    LastName varchar(255),
    UniversityAttended varchar(255),
    CourseTaken varchar(255),
    MarkAchieved varchar(255)
    PRIMARY KEY (ID)

);
/*Here i just made a database and then I made a table*/

-- 2.2
INSERT INTO Sparta (Title, FirstName, LastName, UniversityAttended, CourseTaken, MarkAchieved)
    VALUES
    ('Mr', 'Adam', 'Moussa', 'Brighton University', 'Computer Science', '2:1'),
    ('Mr', 'Atahar', 'Uddin', 'Greenwich University', 'Computer Science', '3rd'),
    ('Mrs', 'Princess', 'Jasmine', 'Magical University', 'Carpet Flying', '1st'),
    ('Dr', 'Jonathan', 'Roberts', 'Cambridge University', 'Medicine', '1st with Distinction');
/*Here, I just added some values into the table in order of the columns*/

-- 3.1
SELECT e.EmployeeID, CONCAT(e.FirstName, ' ', e.LastName) AS "Employee",
    CONCAT(e.FirstName, ' ', e.LastName) AS "Reports to"
FROM Employees e
    LEFT JOIN Employees s ON s.EmployeeID = e.ReportsTo
/*I used this code to find the employee and link them to who they report to. Like previously,
CONCAT was used to bring other columns together into one which was "Employee" and "Reports to"*/

-- 3.2


-- 3.3


-- 3.4
SELECT MONTH(ShippedDate) AS 'Month Shipped',
AVG(DATEDIFF(DD,OrderDate,ShippedDate)) AS 'Time Taken to Ship'
FROM Orders
        GROUP BY MONTH(ShippedDate)
        HAVING AVG(DATEDIFF(DD,OrderDate,ShippedDate)) IS NOT NULL
        ORDER BY [Month Shipped];
/*Please check the excel file for the graph. */
