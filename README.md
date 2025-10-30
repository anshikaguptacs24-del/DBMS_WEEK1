SHOW DATABASES;
CREATE DATABASE IF NOT EXISTS insurance;
USE insurance;


DROP TABLE IF EXISTS participated;
DROP TABLE IF EXISTS owns;
DROP TABLE IF EXISTS accident;
DROP TABLE IF EXISTS car;
DROP TABLE IF EXISTS person;

CREATE TABLE person (
  driver_id VARCHAR(10),
  name VARCHAR(20),
  address VARCHAR(30),
  PRIMARY KEY(driver_id)
);

CREATE TABLE car (
  reg_num VARCHAR(10),
  model VARCHAR(20),
  year INT,
  PRIMARY KEY(reg_num)
);

CREATE TABLE accident (
  report_num INT,
  accident_date DATE,
  location VARCHAR(30),
  PRIMARY KEY(report_num)
);

CREATE TABLE owns (
  driver_id VARCHAR(10),
  reg_num VARCHAR(10),
  PRIMARY KEY(driver_id, reg_num),
  FOREIGN KEY(driver_id) REFERENCES person(driver_id),
  FOREIGN KEY(reg_num) REFERENCES car(reg_num)
);

CREATE TABLE participated (
  driver_id VARCHAR(10),
  reg_num VARCHAR(10),
  report_num INT,
  damage_amount INT,
  PRIMARY KEY(driver_id, reg_num, report_num),
  FOREIGN KEY(driver_id) REFERENCES person(driver_id),
  FOREIGN KEY(reg_num) REFERENCES car(reg_num),
  FOREIGN KEY(report_num) REFERENCES accident(report_num)
);


INSERT INTO person VALUES
('A01', "RICHARD", "SRINIVAS NAGAR"),
('A02', "JOSEPH", "RAJIV NAGAR"),
('A03', "SMITH", "ASHOK NAGAR"),
('A04', "RAVI", "BELGAUM"),
('A05', "ANITA", "MANGALORE");
SELECT * FROM person;

INSERT INTO car VALUES
("KA01AB1234", "HONDA CITY", 2020),
("KA02CD5678", "HYUNDAI I20", 2019),
("KA03EF9012", "MARUTI SWIFT", 2021),
("KA04GH3456", "TOYOTA INNOVA", 2018),
("KA05IJ7890", "TATA NEXON", 2022);
SELECT * FROM car;


INSERT INTO accident VALUES
(10, '2023-06-15', "MG ROAD"),
(11, '2023-07-20', "BRIGADE ROAD"),
(12, '2023-08-05', "INDIRANAGAR"),
(13, '2023-09-19', "KORMANGALA"),
(14, '2023-10-01', "WHITEFIELD");
SELECT * FROM accident;

INSERT INTO owns VALUES 
('A01', "KA01AB1234"),
('A02', "KA02CD5678"),
('A03', "KA03EF9012"),
('A04', "KA04GH3456"),
('A05', "KA05IJ7890");
SELECT * FROM owns;


INSERT INTO participated VALUES
('A01', "KA01AB1234", 10, 15000),
('A02', "KA02CD5678", 11, 20000),
('A03', "KA03EF9012", 12, 18000),
('A04', "KA04GH3456", 13, 30000),
('A05', "KA05IJ7890", 14, 27000);
SELECT * FROM participated;


UPDATE participated 
SET damage_amount = 25000
WHERE reg_num = 'KA03EF9012' AND report_num = 12;


INSERT INTO accident VALUES
(15, '2023-11-01', "JAYANAGAR");


SELECT accident_date, location FROM accident;


SELECT driver_id FROM participated WHERE damage_amount >= 25000;


SELECT * FROM participated ORDER BY damage_amount DESC;


SELECT AVG(damage_amount) FROM participated;


DELETE FROM participated WHERE damage_amount < (SELECT AVG(damage_amount) FROM participated);


SELECT name 
FROM person A 
JOIN participated B ON A.driver_id = B.driver_id 
WHERE damage_amount > (SELECT AVG(damage_amount) FROM participated);


SELECT MAX(damage_amount) FROM participated;# DBMS_WEEK2
