# SQL Fundementals

## Relational Database

Database that is structured to recognise relationships between stored items of information (all the tables are connected in some way)

Structured query languages - SQL (For queries and maintenance)

Orders, Suppliers, Products - these tables are connected because there are relationships within these entities

Each order will have a number of products so they are connected; each product has suppliers so they are connected

**Primary key:**

- identity each record in the table
- must be unique
- cannot be empty
- cannot be changeable
- can be single (single) / multiple columns (composite)
- can only be one per table

**Foreign Key:**

- Reference Primary Keys of other tables
- A table can have any number of Foreign Keys
- Values do not have to be unique
- The RDBMS will prevent any changes that violate the relationship

Data Redundancy - Repeating the same information within the same database (makes it easier to read and access but harder to update)

## Data Modelling

Data model is used to detail how much information is organised

Show relationships between tables

**Three levels:**

- Conceptual - Very broad level business understanding of the data structure
- Logical    - Defines the structure of data elements and relationships between them (independent of the database management system being used
- Physical   - Details the specific implementation of the data model dependant on the actual RDBMS being used

**Conceptual Data Model:**

- Entity names
- Entity Relationships

**Logical Data Model:**

- Entity names
- Entity Relationships
- Attributes
- Primary Keys
- Foreign Keys

**Physical Data Model:**

- Primary Keys
- Foreign Keys
- Table Names
- Column Names
- Column Data Types

**Types of Relationship:**

One-to-One - Reflect the type of connection in which each record only has one relationship to one other record in one other table (vice versa)

One-to-Many - Represents a connection in which one record can have multiple relationships with records in another table

Many-to-Many - Reflect connections in which many records can be related to many records in another table

## Entity Relationship Diagrams (ERD)

ERD - Represents all entities in our data model

- Each entity represented by a table in the database
- Each entity has attributes
- Relationships shown with lines
- Can use Crow's Foot Notation to describe relationships in more detail

Crow's Foot Notation - Represents different types of relationships

## Normalisation

Database Normalisation - Is the process of separating your data out into separate tables.

**Pros:**

- Reduces data redundancy
- Eliminates repeated information
- Increases ease of database maintenance:
- One source of truth for each entry
- Easier Inserts
- Can insert data about single entity
- Easier Deletes
- One location for each delete

**Cons:**

- Increases database depth
- More tables
- Increases difficulty of querying
- Multiple joins required
- More effort for analysts / devs
- More computational effort

Normal Forms - Properties those databases can have which describe the level of normalisation of that database

**First Normal Form (INF):**

- The data must be atomic – data must be presented as small as it possibly can be
- There are no repeated groups
- Each row must be unique

**Second Normal Form (2NF):**

- Already in First Normal Form
- All non-key attributes must be functionally depend upon the full primary key

**Third Normal Form:**

- Already in Second Normal Form
- There are no transitive dependencies – dependency chain

## Database Creation

VARCHAR – Variable character

VARCHAR holds characters (letters, digits, spaces, punctuation, etc…) and the length of each entry can vary, hence variable.

White space – leaving spaces to make it clear to separate each line

```SQL
CREATE TABLE personnel (
    first_name VARCHAR(20)
    last_name VARCHAR(20),
    notes VARCHAR(max),
    phone_number CHAR (11),
    birthdate DATE,
    first_shift_start DATETIME,
    lunhc_break Time,
    number_of_awards INT, -- INTEGER
    hourly_rate DECIMAL(4,2), -- (precision, scale) e.g. 32.15
    height_meters FLOAT(24), -- (max digits) e.g. 3.45e11 (345 billion)
    is_full_time BIT -- e.g. 1 or 0 (true and false)
);
```

Precision – maximum number digits can store

Scale – the number of digits after the decimal point e.g. 32.15

### Inserting Data Into Table

```SQL
DROP TABLE IF EXISTS personnel;
CREATE TABLE personnel (
    first_name VARCHAR(20),
    last_name VARCHAR(20),
    notes VARCHAR(max),
    phone_number CHAR (11),
    birthdate DATE,
    first_shift_start DATETIME,
    lunch_break Time,
    number_of_awards INT, -- INTEGER
    hourly_rate DECIMAL(4,2), -- (precision, scale) e.g. 32.15
    height_meters FLOAT(24), -- (max digits) e.g. 3.45e11 (345 billion)
    is_full_time BIT -- e.g. 1 or 0 (true and false)
);

INSERT INTO personnel (
    first_name, last_name, notes, phone_number,
    birthdate, first_shift_start, lunch_break, number_of_awards,
    hourly_rate, height_meters,
    is_full_time
) VALUES (
    'Joe', --VARCHAR
    'Bloggs', --VARCHAR
    'An excellent employee', --VARCHAR
    '07123456789', --CHAR
    '1990-01-23', --DATE
    '2020-04-01 09:00:00', --DATETIME
    '13:00:00', --TIME
    4, --INT
    12.75, --DECIMAL
    1.77e1, --FLOAT
    1 --BIT
);
```

Null represents a missing or unknown value

Null is not a value

Nothing equals Null

### Primary Key

```SQL
DROP TABLE IF EXISTS courses;

CREATE TABLE courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(20) UNIQUE
);

INSERT INTO courses
(course_id, course_name)
VALUES
(1, 'C# Development'),
(2, 'Java Development'),
(3, 'Data Engineering'),
(4, 'Data ENgineering');
DROP TABLE IF EXISTS courses;

CREATE TABLE courses (
    course_id INT PRIMARY KEY IDENTITY(1,1),
    course_name VARCHAR(20) UNIQUE
);

INSERT INTO courses
(course_name)
VALUES
('C# Development'),
('Java Development'),
('Data Engineering');
```

Primary key automatically added on with ‘Key Identity’

### Foreign Key

```SQL

DROP TABLE IF EXISTS courses;

CREATE TABLE courses (
    course_id INT PRIMARY KEY IDENTITY(1,1),
    course_name VARCHAR(20) UNIQUE
);

INSERT INTO courses
(course_name)
VALUES
('C# Development'),
('Java Development'),
('Data Engineering');

DROP TABLE if EXISTS students;
CREATE TABLE students (
    student_id INT PRIMARY KEY IDENTITY(1,1),
    student_name VARCHAR(20),
    course_id INT FOREIGN KEY REFERENCES courses (course_id)
);

INSERT INTO students
(student_name, course_id)
VALUES
('ALice', 1),
('Bob', 1),
('Charlie', 2),
('David', 5);

DROP TABLE courses;
```

SQL server can prevent against any changes to the database that would break the relationship between the tables

### Altering Tables

```SQL
ALTER TABLE films
ADD budget DECIMAL(10,0), synopsis VARCHAR(200);

ALTER TABLE films
ALTER COLUMN runtime_mins DECIMAL(5,2);

ALTER TABLE films
DROP COLUMN box_office_usd;
```

### Updating Tables

```SQL
DROP TABLE if EXISTS ice_cream;

CREATE TABLE ice_cream (
    id INT,
    flavour VARCHAR(20),
    price DECIMAL(4,2)
);

INSERT INTO ice_cream
(id, flavour, price)
VALUES
(1, 'Vanilla', 3.99),
(2, 'Chocolate Chip', 3.99),
(3, 'Raspberry Ripple', 3.99);

SELECT * FROM ice_cream;

UPDATE ice_cream
SET flavour = 'Mint Chocolate Chip'
Where id = 2;

UPDATE ice_cream
SET price = 4.99
WHERE price = 3.99

DELETE FROM ice_cream
WHERE flavour = 'Raspberry Ripple'
-- WHere id = 3
```
