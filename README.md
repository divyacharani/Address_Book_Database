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