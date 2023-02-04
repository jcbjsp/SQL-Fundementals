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
