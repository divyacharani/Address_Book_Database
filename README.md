# Address_Book_Database

#### Create Address Book Service Database
```
CREATE DATABASE address_book_service;
SHOW DATABASES;
USE address_book_service;
```
#### Create Address Book Table
```
CREATE TABLE address_book (
first_name   VARCHAR(20) NOT NULL,
last_name    VARCHAR(20) NOT NULL,
address      VARCHAR(50) NOT NULL,
city         VARCHAR(20) NOT NULL,
state        VARCHAR(20) NOT NULL,
zip          INT NOT NULL,
phone_number BIGINT NOT NULL,
email_id     VARCHAR(20) NOT NULL,
PRIMARY KEY  (first_name, last_name));
```
#### Add Contacts into Address Book Table
```
INSERT INTO address_book 
(first_name, last_name, address, city, state, zip, phone_number, email_id) VALUES
('Chandler','Bing','M.G.Road','Bangalore','Karnataka',123456,9876543210,'chandler@gmail.com'),
('Joey','Tribiyani','S.R.Nagar','Chennai','Tamil Nadu',234567,7890654345,'joey@gmail.com'),
('Rachel','Green','Begumpet','Hyderabad','Telangana',345678,7896592346,'rachel@gmail.com'),
('Monica','Geller','Thane','Mumbai','Maharashtra',456789,8978765645,'monica@gmail.com'),
('Phoebe','Buffay','Agra','Delhi','Delhi',343423,9934569023,'phoebe@gmail.com');
```

#### Edit Contact using person name
```
UPDATE address_book SET phone_number = 8976897654 WHERE first_name = 'Monica' AND last_name = 'Geller';
UPDATE address_book SET address = 'S.K.Nagar' WHERE first_name = 'Joey' AND last_name = 'Tribiyani';
```

#### Delete contact using person name
```
DELETE FROM address_book WHERE first_name = 'Phoebe' AND last_name = 'Buffay';
```