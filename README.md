# Subqueries-task-6-
CREATE TABLE Country (
    CountryID INT PRIMARY KEY,
    CountryName VARCHAR(255),
    Population INT
);

CREATE TABLE Persons (
    PersonID INT PRIMARY KEY,
    PersonName VARCHAR(255),
    CountryID INT,
    Rating DECIMAL(3, 2),
    FOREIGN KEY (CountryID) REFERENCES Country(CountryID)
);
INSERT INTO Country (CountryID, CountryName, Population) VALUES
(1, 'USA', 331002651),
(2, 'India', 1380004385),
(3, 'Canada', 37742154);

INSERT INTO Persons (PersonID, PersonName, CountryID, Rating) VALUES
(1, 'Alice', 1, 4.5),
(2, 'Bob', 1, 3.2),
(3, 'Charlie', 2, 4.0),
(4, 'David', 2, 2.8),
(5, 'Eve', 3, 3.7);
SELECT Country.CountryName, COUNT(Persons.PersonID) AS NumberOfPersons
FROM Country
LEFT JOIN Persons ON Country.CountryID = Persons.CountryID
GROUP BY Country.CountryName;
SELECT Country.CountryName, COUNT(Persons.PersonID) AS NumberOfPersons
FROM Country
LEFT JOIN Persons ON Country.CountryID = Persons.CountryID
GROUP BY Country.CountryName
ORDER BY NumberOfPersons DESC;
SELECT CountryName 
FROM Country
WHERE CountryID IN (
    SELECT CountryID 
    FROM Persons 
    WHERE Rating = (SELECT AVG(Rating) FROM Persons WHERE CountryID = 1)
);
SELECT CountryName
FROM Country
WHERE Population > (SELECT AVG(Population) FROM Country);
