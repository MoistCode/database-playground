# What is a database (DB)
1. Collection of related information
2. Can be stored in different ways
3. Amount of information
4. Availability
5. How critical
6. Security

# Database management systems (DBMS)
1. Software that helps users create and maintain a DB
2. Manage large amounts of data
3. Handle security
4. Backups
5. Import/export data
6. Concurrency
7. Interacts with software applications
8. Amazon interacts with DB to interact with data (CRUD)
   1. Create
   2. Read
   3. Update
   4. Delete
9. CRUD are main operations with DB

# Two types of DBs
1. Relational DB (SQL)
   1. One or more tables
   2. Each table has columns and rows
   3. *Unique key* identifies each row
   4. Relational database management systems (RDBMS)
      1. Helps users maintain relational database
      2. mySQL, Oracle, postgreSQL, mariaDB, etc.
   5. Structured query language
      1. Standardized language to interact with RDBMS
      2. Used to perform CRUD and other admin tasks
      3. Can define tables and structures
      4. Code is not always portable 
2. Non-relational (noSQL / not just SQL)
   1. Organize data is anything but a traditional table
   2. Key-value pair
   3. Documents (JSON, XML, etc)
   4. Graphs
      1. Relational nodes
   5. Flexible tables
   6. Non-relational database management systems (NRDBMS)
      1. MongoDB, dynamoDB, apache cassandra, firebase, etc.
   7. Implementation specific
      1. Any non-relational database falls under this category
      2. Not NRDBMS implement their own language for performing CRUD and admin ops
   
# Database queries
1. Request made for specific information
2. Complex structure requires complex queries