# SQL-NoSQL-Database-Design
## University Project, First Year Semester 2

Overview: This is a project where I design a MySQL database in the first half, then migrate it to a MongoDB in the second half to conduct some researches.

For further descriptions:
- First part (MySQL database design): view "MySQL Design/Distinction Level Project.pdf" document and this demonstration video: https://www.youtube.com/watch?v=bpLih1vGkDw&ab_channel=DanhNg%C3%B4
- Second part (MongoDB database migration): view "NoSQL Design/High Distinction Level Project.pdf" document.

### Part 1: Relational Database Design
In this project, I have created a relational database named “Classes,” inspired by the timetable at Swinburne University of Technology. The database contains seven entities, each storing various information about class sessions that a student might have. These entities are:
- Convener: Stores personal information about a unit convener.
- Tutor: Stores personal information about a tutor.
- Student: Stores personal information about a student.
- Room: Stores information about a teaching room at Swinburne.
- Unit: Child table of Convener, storing information about a unit at Swinburne.
- Class: Child table of Unit, Room, and Tutor entities, containing information about a particular class at Swinburne.
- Sessions: The weakest entity in the database, a child table of Class and Student tables, storing the enrollment of students into classes at Swinburne.

#### Entity Relationships
The relationships between the entities are as follows:
- Convener – Unit: One convener can manage multiple units (1 to Many). Each unit is managed by one convener (1 to 1).
- Unit, Room, Tutor – Class: One unit, room, or tutor can be associated with multiple classes (1 to Many). Each class is associated with one unit, room, and tutor (1 to 1).
- Class, Student – Sessions: One class or student can be associated with multiple sessions (1 to Many). Each session is associated with one class and one student (1 to 1).

####UML Entity Relationship Diagram
The UML Entity Relationship Diagram visually represents the relationships and entities described above.
![image](https://github.com/DanNgo4/SQL-NoSQL-Database-Design/assets/127183060/fd9422f2-b4a1-4484-8d5e-6fea6108b37e)

#### Normalisation Design
The database design follows normalisation principles to ensure data integrity and reduce redundancy:
- First Normal Form (1NF): All tables have no repeating groups, and the attributes are atomic.
- Second Normal Form (2NF): No table has partial dependencies among non-primary attributes. Each table has one surrogate primary key, and the Sessions table has no non-primary attributes.
- Third Normal Form (3NF): There are no transitive dependencies in any table, as most tables only have one surrogate key, and one table contains only composite keys.

#### Database Implementation
The database was implemented with the following tables:
- Convener: Stores personal details of conveners.
- Unit: Stores information about units and references the Convener table.
- Tutor: Stores personal details of tutors.
- Room: Stores details about rooms, including capacity.
- Class: Stores information about classes and references Unit, Tutor, and Room tables.
- Student: Stores personal details of students.
- Sessions: Stores enrollment details and references Class and Student tables.
  
#### Inserting Data Records
Data was inserted into each table to represent conveners, units, rooms, tutors, classes, students, and session enrollments.

#### Results
The database was populated with data, and various queries were executed to retrieve information about class sessions, tutors, units, and student enrollments.

#### Queries Using JOIN and GROUP Operations
Five complex queries were written using JOIN and GROUP operations to retrieve specific information from the database:
- Query 1: Retrieves detailed information about class sessions with at least one student attending.
![image](https://github.com/DanNgo4/SQL-NoSQL-Database-Design/assets/127183060/592d29ff-ac89-48e4-8012-05f1a400e675)

- Query 2: Retrieves tutors who have classes on Monday.
![image](https://github.com/DanNgo4/SQL-NoSQL-Database-Design/assets/127183060/7816140d-2fd4-4f20-abf7-6f823a588806)

- Query 3: Retrieves all classes ordered by the number of attending students.
![image](https://github.com/DanNgo4/SQL-NoSQL-Database-Design/assets/127183060/3c0c5ee0-d8de-4202-840d-376916d4a4f0)

- Query 4: Retrieves the number of students enrolled in classes of each unit.
![image](https://github.com/DanNgo4/SQL-NoSQL-Database-Design/assets/127183060/882b8c74-651b-4348-8c04-7cc7ba227a39)

- Query 5: Retrieves the number of students that each tutor is teaching every week.
![image](https://github.com/DanNgo4/SQL-NoSQL-Database-Design/assets/127183060/54016dc8-7cac-4751-94c1-6c0002689294)

### Part 2: Data Migration and Comparison between MySQL and MongoDB
In this report, I will use the custom database called “Classes,” which I implemented in my Distinction Level Project. The aim is to migrate this database to a MongoDB database and compare the differences in data storage between the two DBMSs.

#### Data Migration
- MySQL: As a table-based system, MySQL organises data into structured tables, facilitating efficient data querying and searching. Creating entities and inserting data in MySQL requires adherence to strict rules regarding primary keys, foreign keys, and data integrity, ensuring a well-defined relational structure.
- MongoDB: In contrast, MongoDB is a document-based non-relational DBMS, which provides greater flexibility in handling different types of data, such as unstructured or semi-structured data. Unlike MySQL, MongoDB does not impose strict ordering for creating tables and inserting data. Objects are stored in documents within collections, allowing for a more flexible and dynamic data model.

#### Data Storage
- MongoDB: Each individual record in MongoDB is stored as a document. These documents, which can contain embedded objects, belong to specific collections. The hierarchical structure of a MongoDB document can be more complex than a row in a MySQL table, allowing for nested data structures.
- MySQL: In MySQL, records are stored as rows or tuples in structured tables. All records within a table adhere to the same schema, making data querying straightforward. MySQL's relational model ensures that data is organised in a consistent and predictable manner.

#### Data Query Performance
- Comparing the performance of MySQL and MongoDB can be challenging due to their fundamentally different approaches to data organisation and querying.
- MySQL: Known for executing high-performance JOIN operations across multiple well-indexed tables, MySQL is efficient at handling complex queries involving multiple tables.
- MongoDB: While MongoDB supports similar functionality through the $lookup operation, its design philosophy typically minimises the need for joins. By organising data in a hierarchical model and embedding related data within a single document, MongoDB often reduces the necessity for cross-document joins, focusing instead on the flexibility and ease of accessing nested data.

#### Conclusion
In this report, I have briefly compared MySQL, a relational database, with MongoDB, a non-relational database, using a database initially designed in MySQL. To conclude, MongoDB offers greater flexibility in data storage, making it suitable for handling a variety of data types. However, this flexibility may come at the expense of some security and data integrity features inherent to the structured SQL databases like MySQL. The choice between these two powerful DBMSs depends on specific user requirements, organisational needs, and scenarios, highlighting their unique strengths in storing, sorting, and presenting data for software development.
