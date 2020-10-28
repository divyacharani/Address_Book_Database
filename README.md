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

#### Retrieve a Particular Contact
```
SELECT * FROM address_book WHERE city = 'Bangalore' OR state = 'Karnataka';
```

#### Retrieve count of contacts by city and state
```
SELECT city, COUNT(first_name) FROM address_book GROUP BY city;
SELECT state, COUNT(first_name) FROM address_book GROUP BY state;
```

#### Retrieve contacts order by person name for a given city
```
SELECT * FROM address_book WHERE city = 'Mumbai' ORDER BY first_name;
```

#### Add address book name and type
```
ALTER TABLE address_book ADD book_name VARCHAR(20) NOT NULL;
ALTER TABLE address_book ADD type VARCHAR(20) NOT NULL;
UPDATE address_book SET book_name = 'myContacts', type='Friends' WHERE first_name = 'Joey';
UPDATE address_book SET book_name = 'myContacts', type='Profession' WHERE first_name = 'Rachel';
UPDATE address_book SET book_name = 'myContacts', type='Profession' WHERE first_name = 'Monica';
UPDATE address_book SET book_name = 'myContacts', type='Family' WHERE first_name = 'Chandler';
```

#### Retrieve contacts count by book type
```
SELECT type, COUNT(first_name) FROM address_book GROUP BY type;
```

#### Add person to both family and friend
```
ALTER TABLE address_book DROP PRIMARY KEY;
ALTER TYPE address_book ADD PRIMARY KEY (first_name, last_name, type);
 INSERT INTO address_book 
(first_name, last_name, address, city, state, zip, phone_number, email_id, book_name, type) VALUES 
('Rohith','Sharma','K.T.Nagar','Bangalore','Karnataka',347621,7890654567,'rohith@gmail.com','myContacts','Friends');
 INSERT INTO address_book 
(first_name, last_name, address, city, state, zip, phone_number, email_id, book_name, type) VALUES 
('Rohith','Sharma','K.T.Nagar','Bangalore','Karnataka',347621,7890654567,'rohith@gmail.com','myContacts','Family');
```

#### Implement ER Diagram
```
DROP TABLE address_book;
CREATE TABLE contact (
    contact_id INT NOT NULL,
    first_name VARCHAR(20) NOT NULL,
    last_name VARCHAR(20) NOT NULL,
    address VARCHAR(250) NOT NULL,
    city VARCHAR(20) NOT NULL,
    state VARCHAR(20) NOT NULL,
    zip INT NOT NULL,
    phone_number BIGINT NOT NULL,
    email_id VARCHAR(20) NOT NULL,
    PRIMARY KEY (contact_id)
);

CREATE TABLE address_book_name (
    book_id INT NOT NULL,
    book_name VARCHAR(20) NOT NULL,
    PRIMARY KEY (book_id)
);


CREATE TABLE address_book_type (
    type_id INT NOT NULL,
    type_name VARCHAR(20) NOT NULL,
    PRIMARY KEY (type_id)
);


CREATE TABLE dictionary (
    contact_id INT NOT NULL,
    book_id INT NOT NULL,
    type_id INT NOT NULL,
    FOREIGN KEY (contact_id) REFERENCES contact (contact_id),
    FOREIGN KEY (book_id) REFERENCES address_book_name (book_id),
    FOREIGN KEY (type_id) REFERENCES address_book_type (type_id)
);
```
#### Insert data into tables
```
INSERT INTO contact  VALUES
(1, 'Chandler','Bing','M.G.Road','Bangalore','Karnataka',123456,9876543210,'chandler@gmail.com'),
(2, 'Joey','Tribiyani','S.R.Nagar','Chennai','Tamil Nadu',234567,7890654345,'joey@gmail.com'),
(3, 'Rachel','Green','Begumpet','Hyderabad','Telangana',345678,7896592346,'rachel@gmail.com'),
(4, 'Monica','Geller','Thane','Mumbai','Maharashtra',456789,8978765645,'monica@gmail.com'),
(5, 'Phoebe','Buffay','Agra','Delhi','Delhi',343423,9934569023,'phoebe@gmail.com');

INSERT INTO address_book_name VALUES
(101, 'myContacts'),
(102, 'officeContacts');

INSERT INTO address_book_type VALUES
(50, 'Family'),
(51, 'Friend'),
(52, 'Professional');

INSERT INTO dictionary VALUES
(1,101,50),
(2,101,51),
(3,101,50),
(4,101,50),
(5,102,52);
```

#### Retrieve Contact Details
```
SELECT * FROM contact WHERE city = 'Bangalore' OR state = 'Karnataka';

SELECT city, COUNT(contact_id) FROM contact GROUP BY city;
SELECT state, COUNT(contact_id) FROM contact GROUP BY state;

SELECT * FROM contact WHERE city = 'Mumbai' ORDER BY first_name;

SELECT address_book_type.type_name, COUNT(dictionary.contact_id) FROM dictionary
INNER JOIN address_book_type ON address_book_type.type_id = dictionary.type_id
GROUP BY dictionary.type_id;
```
