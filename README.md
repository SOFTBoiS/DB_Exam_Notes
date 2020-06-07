# Database Questions

[All Database Types](#All-Database-Types)  
[SQL Databases](#SQL-Databases)  
[Document Databases](#Document-Database)  
[Column-Oriented Database](#Column-Oriented-Database)  
[Key-Value Data Store](#Key-Value-Data-Store)

## All Databases

### 1) Explain the following terms: data, information, database, and database management system. What is the difference? Give examples.

- **Information** describes entities. For example: User information, city information, computer information.
- **Data** is information that is stored on a computer. For users this could be: name, username, age etc. for a computer it could be: gpu, cpu, ram etc.
- A **database** stores data in a structured manner so it can easily be accessed and mutated.
- A **DBMS** is software used to interact with a database, such as performing CRUD operations on data.

### 2) What is called a database schema? Which databases enable enforcing a hard schema, which are schemaless, and which enable storing semi-structured data?

A **schema** is the data structure of a database table, in RDBMS, such as PostgreSQL, every database table should have a fixed data structure.

**Schemaless** means the database don't have fixed data structure, such as MongoDB, it has JSON-style data store, you can change the data structure as you wish.

SQL Databases (we have worked with):

- PostgreSQL
- MySQL

NoSQL Databases (we have worked with):

- MongoDB
- Redis
- CouchDB
- Neo4j
- HBase

MongoDB uses JSON which is a **semi-structured** data.

### 3) Explain the difference between logical data model and underlying physical data storage organisation. Give examples for some of the databases you are familiar with.

![](https://i.imgur.com/ZVIQ7Ls.png)

Logical
![](https://www.guru99.com/images/1/022218_0657_WhatisDataM3.png)

Physical
![](https://www.guru99.com/images/1/022218_0657_WhatisDataM4.png)

### 4) What is called a database transaction? Which are the main properties of a transaction? Explain ACID properties.

A **database transaction** is a unit of work that is either completed as a unit or undone as a unit.  

**A**tomic - All or nothing  
**C**onsistency - All data will be valid according to all defined rules  
**I**solation - No transaction will be affected by any other transaction  
**D**urability - Once a transaction is committed, it will remain in the system  

A transactions is a procedure where a query only can have a success with and correct modified database, or a rollback where all modifications is returned to the state before the transaction started.  

A rollback is triggered if an error or custom condition is reached. When this happens the changes from the given transaction query will be undone. Checkpoints can be made to control the roll back.

**Atomic**  
The whole transaction can be seen as one unit, if one thing fails the whole thing fails.

**Consistency**  
Ensures the database constantly is in a valid state. 

**Isolation**  
The transaction is isolated and everything and it cant be modified from external sources.

**Durability**  
After the transaction is committed the data is stored and cant be rolled back.

### 5) Explain the concurrency problem in database implementation and the techniques for controlling it. How does it relate to transaction management and isolation? Which are the basic transaction isolation levels?

[ref](https://www.geeksforgeeks.org/concurrency-control-techniques/)
There's four techniques to control:  
- Two-Phase Locking Protocol
- Time Stamp Ordering Protocol
- Multi Version Concurrency Control
- Validation Concurrency Control 

|Isolation Level|Dirty Reads|Non-Repeatable Reads|Phantom Reads|  
|---|---|---|---|  
|Read Uncommitted|✅|✅|✅|  
|Read Committed|⛔️|✅|✅|  
|Repaatable Read|⛔️|⛔️|✅|  
|Serializable|⛔️|⛔️|⛔️|  

**Dirty read:**  
A transaction reads data written by a concurrent uncommitted transaction.

**Nonrepeatable read:**  
A transaction re-reads data it has previously read and finds that data has been modified by another transaction (that committed since the initial read).

**Phantom read:**  
A transaction re-executes a query returning a set of rows that satisfy a search condition and finds that the set of rows satisfying the condition has changed due to another recently-committed transaction.


### 6) What is the purpose of indexing the database? How do indices operate? Give some examples of guidance rules of indexing.

 1 -> 26  
 2 -> 23  
 3 -> 1  
 4 -> 25  
 5 -> 21

### 7) How to ensure high quality of database model and validate a database? Name some validation techniques. Give examples of validation against user transactions?
You set restrictions on your data (type etc.) then validate by creating a user transaction and validating only valid data can be inserted.  
Data analysis  
Søndag

### 8) Name some criteria for database operations performance. How to estimate the cost of an operation? Name some techniques for performance optimization.

Big O

Explain analyze
Normalization vs denormalization
Indexing
Subquery vs join (cartesian product)  
**Cartesian product**
![](https://cdn.discordapp.com/attachments/677165328438132769/718740582779977738/1200px-Cartesian_Product_qtl1.png)

### 9) What is called transaction log, what does it contain and how to use it?

[ref](https://en.wikipedia.org/wiki/Transaction_log)

The transaction log record all transactions made on the database. It is used to bring the database back to a consistent state after a system failure.

These logs are also used when roll back operations occur.

### 10) Explain the scope of data security and protection. Name some major security threats. Describe approaches and measures of securing a database. Name some hardware methods of data protection.

Privileges (User/Roles)

Encrypt data (passwords, credit card etc.)

Views (User ser ikke data direkte) - don't return the correct ids from DB

**Excessive** privileges. When workers are granted default database privileges that exceed the requirements of their job functions, these privileges can be abused, Gerhart said. “For example, a bank employee whose job requires the ability to change only account holder contact information may take advantage of excessive database privileges and increase the account balance of a colleague’s savings account.” Further, some companies fail to update access privileges for employees who change roles within an organization or leave altogether.

**Database Injections** (fx SQL injection) check on backend (prepared statements for SQL and NoSQL)

**Storage media exposure**. Backup storage media is often completely unprotected from attack, Gerhart said. “As a result, numerous security breaches have involved the theft of database backup disks and tapes. Furthermore, failure to audit and monitor the activities of administrators who have low-level access to sensitive information can put your data at risk. Taking the appropriate measures to protect backup copies of sensitive data and monitor your most highly privileged users is not only a data security best practice, but also mandated by many regulations,” he said.

### 11) What is the meaning of the CAP theorem? How does it differ from the ACID rules?

![](https://i.imgur.com/tLsz4FQ.png)

**ACID consistency** is all about database rules. If a schema declares that a value must be unique, then a consistent system will enforce uniqueness of that value across all operations.

**CAP consistency** promises that every replica of the same logical value, spread across nodes in a distributed system, has the same exact value at all times.

ACID - All or nothing  
CAP - Choose two

AP DBs: You always get an answer, but you are not certain it is the last updated answer (example: You fetch row 1 from node 1 but someone just updated row_1 on node 2. You get an answer, but not the updated one.)

CP DBs: You always make sure you get the correct answer, but fails if it cant make sure its the updated data 

### 12) Explain how to choose an appropriate database type for an application.

**Relational**  
Relational databases is great for data with a static schema and relations. (User information, product information, banking) 
  
**Graph Oriented**  
If the data structure is network like and graph algorithms could improve your business intelligence. (Good for highly connected data)
  
**Document**  
If you have a dynamic schema and don't focus on normalization and relations. (historic, datastructure might change)
  
**Key Value Data Store**  
If you want a fast but limited database, where speed is the focus and data consistency isn't. (sessions, shopping carts, simple structure?)
  
**Column Oriented**  
If you are working with big data, this one is made for you. (Statistics with big data. Google searches, items clicked on in a e-commerce site etc.)

## SQL Databases

### 13) What is called relational data model? Which are the model’s components? What is the difference between relation and relationship? Which are the properties of a relationship?  

ER-diagram  
Relation == Table  
Relationship == How two or more relations are connected (Many-to-Many, One-to-Many, One-to-One)

### 14) Which mathematical theory stays behind the relational data models? Which theoretical terms are used for describing the model and its components?

- Columns - A domain of values of a certain type, sometimes called an _attribute_
- Rows - An object comprised of a set of column values, sometimes called a _tuple_
- Tables - A set of rows with the same columns, sometimes called a _relation_

[måske noget info her](https://piazza.com/class_profile/get_resource/j74smf7qnr1x8/j7kquucg4ih4av)

### 15) What is called relational algebra? How is it related to database development? Which relational operations can be performed in a database? Name some unary and binary operations.

relational operators:
* \>
* <
* =
* \>=
* <=
* != , <> ,  ~=

https://www.tutorialspoint.com/dbms/relational_algebra.htm
[Relational Algebra](https://slideplayer.com/slide/8666326/)
![[Relational Algebra](https://slideplayer.com/slide/8666326/) slide 4](https://images.slideplayer.com/26/8666326/slides/slide_4.jpg)
![[Relational Algebra](https://slideplayer.com/slide/8666326/) slide 5](https://images.slideplayer.com/26/8666326/slides/slide_5.jpg)

### 16) Which are the main programming units in SQL? Explain the difference between them. What are the advantages of using SQL programming units?

Triggers, Stored Procedure and Functions

Procedure: Insert, Update and Delete (Call procedure_name())
Function: Select (Select function_name())

Begin - End (uses transaction)

Quality of Life (dont have to write the same long transactions if you know you're going to use them often)

Functions and Procedures provides a better security because the input arguments are requeired and cant be invalid. This can be obtained by setting priviliges only to use these.

Low coupling (if can be used multipe places) (refactoring)

### 17) Which are the stages of database development methodology? Which are their objectives, tasks, tools and techniques? At which stage are the database requirements specified? Which tasks are solved at the design stage? Which are the three design layers? How do they differ?

Analysis -> Conceptual database design -> requirements specified  
Logical Design  
Implementation -> physical design?  
Realizing the Design -> creation of the DB  
Populating the Database

the three design layers:
* conceptual
* logical
* physical

### 18) What are the purpose and the content of the data dictionary? What are the candidate key, primary key, and composite key. What is the use of them?

[ref](https://www.bridging-the-gap.com/data-dictionary/)

 Data Dictionary provides information about each attribute, also referred to as fields, of a data model. An attribute is a place in the database that holds information. For example, if we were to create a Data Dictionary representing the articles here on Bridging the Gap, we’d potentially have attributes for article title, article author, article category, and the article content itself.

A Data Dictionary is typically organized in a spreadsheet format. Each attribute is listed as a row in the spreadsheet and each column labels an element of information that is useful to know about the attribute.

Let’s look at the most common elements included in a data dictionary.

* Attribute Name – A unique identifier, typically expressed in business language, that labels each attribute.
* Optional/Required – Indicates whether information is required in an attribute before a record can be saved.
* Attribute Type – Defines what type of data is allowable in a field. Common types include text, numeric, date/time, enumerated list, look-ups, booleans, and unique identifiers.

---

* Primary key == A value that uniquely represents a row(tuple) in a realation(table)
* Candidate key == Unique
* Composite key == is a combination of two or more columns in a table that can be used to uniquely identify each row in the table when the columns are combined uniqueness is guaranteed, but when it taken individually it does not guarantee uniqueness.

### 19) What is the meaning of functional dependency? Explain the implementation of it. Give examples. How does it relate to database normalization?

Functional dependency is that one column is dependent of another.  

Between zip code and city a zip code decides the value of city.  

For 2nd normal form you remove all partial dependencies.  
For 3rd normal form you remove all transitive dependencies.  

|Employee number | Employee Name | Salary |      City     |
|----------------|---------------|--------|---------------|
|1               | Dana          | 50000  | San Francisco |
|2               | Francis       | 38000  | London        |
|3               | Andrew        | 25000  | Tokyo         |

In the example above, if we know the value of Employee number, we can obtain Employee Name, city, salary, etc. By this, we can say that the city, Employee Name, are functionally depended on Employee number.

|Company   | CEO           |Age|
|----------|---------------|---|
|Microsoft | Satya Nadella | 51|
|Google    | Sundar Pichai | 46|
|Alibaba   | Jack Ma       | 54|

### 20) What is the purpose of database normalization? Which are the basic normal forms of a relation? What is the purpose of database de-normalization? Give examples for implementation of de-normalization techniques.

Normalization is a systematic approach of decomposing tables to eliminate data redundancy(repetition) and undesirable characteristics like Insertion, Update and Deletion Anomalies. It is a multi-step process that puts data into tabular form, removing duplicated data from the relation tables.  

Normalization is used for mainly two purposes:  
* Eliminating redundant(useless) data.  
* Ensuring data dependencies make sense i.e data is logically stored.  

**Normal Forms:**
* UNF - Primary key and no repeating group
* 1NF - Atomic columns (Only one value in a column)
* 2NF - Avoid partial dependencies (Dependent on a part of a composite primary key)
* 3NF - Avoid transitive dependencies (Dependent on something other than a primary key)
* EKNF - Every non-trivial functional dependency involves either a superkey or an elementary key's subkey
* BCNF - No redundancy from any functional dependency

For each relation:  
Every non-key attribute  
depends on the key (1st normal form)  
the whole key (2nd normal form)  
and nothing but the key (3rd normal form)  
so help me Codd.

You could denormalize tables where you normally would have to do a lot of joins, because you often would need to use the data together. This way your queries would be faster at the cost of data redundancy.

### 21) What is referential integrity and why is it important? Give examples of methods for supporting the referential integrity.

For example, if we delete record number 15 in a primary table, we need to be sure that there’s no foreign key in any related table with the value of 15

Cascade handles this

### 22) What is the purpose of data locking? Which database resources are lockable? What is called deadlock and how to avoid it?

Isolation levels can create issues such as `Dead Locks` this is a state where to transactions waits for the other to give them access to what ever data there has ben locked. Some systems handles dead locks and "kills" the one with the least effect on the database also called the victim and respond with an error code 1205.  

You can avoid deadlocks by ordering your SQL queries. Always execute your SQL queries in the same order.  
When creating indexes you can create them concurrently to avoid locks for large periods of time.

### 23) Which data is called derived data? What is called database view? What are the advantages and limitations of using views? Name one advantage of view parametrisation. Name one disadvantage of view materialization.

[ref](http://www.advancesharp.com/blog/1104/parameterized-view-in-sql-server-with-example)
derived data -> INGEN DATA OM DATA I BASEN  
**Views:**  
Materialized view = You save the view to an actual table.  
The data you get from the materialized view, is only as up to date as the last time you materialized the view.

### 24) Explain how SQL queries are executed by a database server. Explain what is an execution plan, how is it built and used? What is the difference between the estimated and actual execution plans?

[ref](https://datsoftlyngby.github.io/soft2020spring/resources/cf77692e-SQLDBPerformance1-Indexing.pdf) slide 5-11

Estimated = estimated
Actual = actual
![](https://i.imgur.com/fkpbl7G.png)  
Den her nedenunder kan måske også bruges ved #25:
![](https://i.imgur.com/gO1XuyF.png) 


### 25)* What are the objectives of query optimisation? How can a developer support it? What are the roles of SARGs and JOINs in query optimization?

![](https://i.imgur.com/h73wbDm.png)
![](https://i.imgur.com/04OTJIh.png)
Use your JOINs and WHERE clauses when querying data, instead of doing it after to limit the data size.

### 26) What does ORM stay for? How is it used? Name some ORM programming instruments. What is known as Impedance Mismatch? Which are the mismatches between object data model and relational data model?

**O**bject **R**elational **M**apping

* Django
* SQLAlchemy
* JPA (Jakarta Persistence API)

[ref](https://www.geeksforgeeks.org/impedance-mismatch-in-dbms/)
Impedance mismatch is the term used to refer to the problems that occurs due to differences between the database model (tuples) and the programming language model (objects). The practical relational model has 3 components these are:

* Attributes and their data types (columns)
* Tuples (rows)
* Tables

### 27) What are the strengths and weaknesses of RDB? When is RDB the best choice of database type and when it should be avoided? Name some typical use cases and applications.

**Pros:**
* Static Schema
* Need referential integrity
* Need to enforce ACID principles
* Vertical scaling
 
**Cons:**
* Many relations = Neo4j (graph)
* Not good for data where the structure can change
* Horizontal scaling

Vertical, 1 maskine gøres bedre.  
Horizontal, split dataen over flere maskiner.  
![](https://i.imgur.com/Vp61HPy.png)


## NoSQL Databases

### 28) What stays behind the abbreviation NoSQL? How have the NoSQL databases originated? Which are the main differences between SQL and NoSQL databases?

**N**ot **O**nly **SQL**

SQL: Permitted Schema
NoSQL: Schemaless

STORY
The term “NoSQL” first appeared in 1998, used to describe a relational database developed by Carlo Strozzi that provided no form of the SQL language for querying

NoSQL developed at least in the beginning as a response to web data, the need for processing unstructured data, and the need for faster processing.

### 29) Describe four major types of NoSQL databases and their appropriate implementations. Name one representative database of each type.
 
Document - Mongo
Key/Value - Redis
Graph - Neo4j (Social network, facebook, twitter)
Column - HBase
  
**Graph Oriented**  
If the data structure is network like and graph algorithms could improve your business intelligence. (Good for highly connected data)
  
**Document**  
If you have a dynamic schema and don't focus on normalization and relations. (historic, datastructure might change)
  
**Key Value Data Store**  
If you want a fast but limited database, where speed is the focus and data consistency isn't. (sessions, shopping carts, simple structure?)
  
**Column Oriented**  
If you are working with big data, this one is made for you. (Statistics with big data. Google searches, items clicked on in a e-commerce site etc.)

### 30) What type of a databases is used for handling large volumes of unstructured data?

schemaless
column-oriented
document-oriented

### 31) Name some criteria for comparison the NoSQL databases. How do they compare CAP-wise?

![](https://i.imgur.com/tLsz4FQ.png)

### 32) What is known as Big Data? Which are the basic features of it? Which big data processing technologies you are familiar with?

[ref](https://www.irjet.net/archives/V4/i9/IRJET-V4I957.pdf)

**Volume**  
The size of the data. Puts the word big in Big Data.
  
**Variety**  
The different type of data.
  
**Velocity**  
The speed the data is produces.

Hadoop

### 33) Explain Map-Reduce concept. Which databases provide support for it? Give an example of implementation.

MongoDB

_mongo shell_
```javascript
db.collection.mapReduce(
    <MAP FUNCTION>,
    <REDUCE FUNCTION>,
    <QUERY>,
)
```

I can't use HBase but found this [source](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/mapreduce/package-summary.html )

### Column-Oriented Database

#### 34) What type of database is HBase? Which are the main features of it and what is their impact? Which CAP features are supported by HBase?

No-SQL column oriented database. 

- Linear and modular scalability.
- Strictly consistent reads and writes.
- Automatic and configurable sharding of tables
- Automatic failover support between RegionServers.
- Convenient base classes for backing Hadoop MapReduce jobs with Apache HBase tables.
- Easy to use Java API for client access.
- Block cache and Bloom Filters for real-time queries.
- Query predicate push down via server side Filters
- Thrift gateway and a REST-ful Web service that supports XML, Protobuf, and binary data encoding options
- Extensible jruby-based (JIRB) shell
- Support for exporting metrics via the Hadoop metrics subsystem to files or Ganglia; or via JMX

CP

#### 35) How does HBase differ from SQL databases? How does it support transactions and indexing?
Column vs row oriented.
Hbase saves columns together on the disk, so it is much faster to read all elements in the same column, rather than looking for a specific row.

Index:
https://stackoverflow.com/questions/35771996/indexing-process-in-hadoop
Hadoop does not indexing. With these sizes of datasets regenerating indexes are too costly, so changing data will be a hassle. 
HDFS can do file based indexing and inputsplit based indexing. Inpusplit inData is stored in blocks of 128mb, and each of those blocks are indexed. Another option is to index by incoming files, and not split them up

Transaction:
Only supports single row transactions

![](https://i.imgur.com/kjuqBnT.png)

#### 36) Which is the underlying storage model HBase uses? Which are the advantages of such a model?
[ref](https://hadoop.apache.org/docs/r1.2.1/hdfs_design.html)
HDFS is highly fault-tolerant and is designed to be deployed on low-cost hardware.  
HDFS provides high throughput access to application data and is suitable for applications that have large data sets.

Splits data onto different nodes (almost RAID 10, but instead of spreading out to different disks in the same system, it splits it to different server racks where several systems run) https://www.youtube.com/watch?v=NeqC6t1J1dw
This gives both speed and makes it less prone of data loss (However if all nodes with same data fails, data is lost)

#### 37) Explain HBase scalability model. What is the role of HMaster, Region Server, and Zookeeper?

Hmaster responsible of load balancing and assigning regions to region servers. DDL operations are handled by HMaster. Also monitors regionservers
Zookeeper 
Region server responsible for read/write requests for their respective regions
Tables split into difference regions. Regions store range og key value pairs

#### 38) Which are the available work modes for HBase? How are the read and write operations performed?

Standalone which is for testing purposes. For production environment you should use distributed mode. This makes hbase daemons run on multiple servers in a cluster. Read writes are striped between 2 nodes running on same server rack and duplicated to another node in a server rack.

Write:
1. The Client sends a write data request to the HregionServer through the Zookeeper, and writes the data in the Hregion
2. The data is written to the MemStore of Hregion
3. When the MemStore reaches the preset threshold, the data is flushed into a StoreFile
4. when the size of the StoreFile reaches a certain threshold, it is split and divided into to StoreFiles
5. When the number of StoreFile files increases to a certain threshold, the Comapct merge operation is triggered, and multiple StoreFiles are merged into one StoreFile.
    - StoreFiles gradually forms a large Storefile through the continuous Compact operation
6. After the size of a single StoreFile exceeds a certain threshold, the Split operation is triggered to split the current Hregion into two new Hregions
    - The parent HRegion will go offline, and the two sub-HRegions will be assigned to the corresponding HregionServer by HMaster so that the pressure of the original HRegion can be shunted to the two HRegions

Read:
1. Client accesses Zookeeper to obtain the META table
2. From the META table the corresponding HRegionServer and HRegion are found
3. First the requested data is searched in a memory store called BlockCache, which keeps data from previous reads
4. If the data is not found in BlockCache, the MemStore, and then the StoreFile are searched respectively
5. When the data is found, it is written in BlockCache for further reads, and send back to the client

#### 39) What are the strengths and weaknesses of HBase? When is HBase the best choice of database type and when it should be avoided? Name some typical use cases and applications.

Pros:  
- Schema-less
- linear scalability
- fast lookups for large tables

Cons:  
- Single row transactions only
- Uses API for processing data
- indexing on row key only

Big Data
If you are working with big data, this one is made for you. (Statistics with big data. Google searches, items clicked on in a e-commerce site etc.)


### Document Database

#### 40) What type of database is MongoDB? Which data model does it use? How does it differ from RDB?
MongoDB is a document based database. This database consist of collections (tables) and documents (rows).

MongoDb is preferred to be denormalized where as RDB is preferred to be normalized. THere is no permitted schema in mongoDB but one can be applied. It Stores its data in BSON which is a binary format of JSON, and uses a JSON-like data structure.


#### 41) Which language is MongoDB written in? (Javascript, C, C++)

C++, Javascript, Python
[Link to github](https://github.com/mongodb/mongo)
![](https://i.imgur.com/0VZwgom.png)


#### 42) Is MongoDB classified as a NoSQL database?

Yes

#### 43) Which format is supported by MongoDB? (SQL, XML and/or BSON)

BSON

#### 44) Is MongoDB a graph, key value and/or a document database that provides high performance, high availability, and easy scalability?

Document Database

#### 45) How does MongoDB provide high availability?

MongoDB is a CP-database and uses *shards* to ensure high availability.

#### 46) Can MongoDB be used as a file system? Can MongoDB run over single servers only?

Yes FS no to other

![](https://i.imgur.com/GsjK6c6.png)


MongoDB can run over multiple servers, balancing the load and/or duplicating data to keep the system up and running in case of hardware failure.

Yes, it has something called GridFS (Grid File System) that handles large files.

#### 47) When MongoDB scales horizontally using sharding for load balancing purpose, who chooses the shard key, which determines how the data in a collection will be distributed?

[ref](https://hub.packtpub.com/mongodb-sharding-clusters-choosing-right-shard-key/#:~:text=The%20primary%20shard%20is%20different,at%20the%20moment%20of%20creation.)

The primary shard is automatically selected by MongoDB when we create a new database in a sharded environment. MongoDB will pick the shard that has the least data stored at the moment of creation.

"The user (developer) chooses a shard key, which determines how the data in a collection will be distributed"

#### 48) Is it correct that the primary replica performs all writes and reads by default?
https://docs.mongodb.com/manual/core/replica-set-primary/
![Replica Set](https://i.imgur.com/raD6Jen.png)

Yes, by default. However all members of the replica set can accept read operations if configured so.

*note:* the primary is the only member in the replica set that receives **write** operations
![](https://i.imgur.com/F2x75fF.png)

#### 49) Is it correct that data in MongoDB has a flexible schema?

Yes, mongoDB has a dynamic schema, but can be configured to have a static one.

[schema validation](https://docs.mongodb.com/manual/core/schema-validation/)

#### 50) In MongoDB, at which level are write operations atomic?

[write operations atomicity](https://docs.mongodb.com/manual/core/write-operations-atomicity/)
Write operations are atomic at the document level.  
Every write to a document is considered atomic, so in case of using `db.collection.updateMany()` where multiple documents are modified, only the document modifications are seen as atomic.

#### 51) Explain how MongoDB processes collection of documents using Map-Reduce operations. Explain the phases in MongoDB’s Map-Reduce. What would be the maximum document size for results of Map-Reduce operation?

_mongo shell_
```javascript
db.collection.mapReduce(
    <MAP FUNCTION>,
    <REDUCE FUNCTION>,
    <QUERY FILTER>,
)
```
[ref](https://docs.mongodb.com/manual/core/map-reduce/)
MongoDB applies the map phase to each input document (i.e. the documents in the collection that match the query condition). The map function emits key-value pairs. For those keys that have multiple values, MongoDB applies the reduce phase, which collects and condenses the aggregated data. MongoDB then stores the results in a collection. Optionally, the output of the reduce function may pass through a finalize function to further condense or process the results of the aggregation.
The maximum (BSON) document size is 16mb per document in MongoDB.  
The maximum document size helps ensure that a single document cannot use excessive amount of RAM  
[MongoDB limits](https://docs.mongodb.com/manual/reference/limits/)

#### 52) How does MongoDB support transaction management?

https://docs.mongodb.com/manual/core/transactions

On single documents Mongo is atomic by nature - however when there are multiple documents you'll need to use multi-document transactions.

"Multi-document transactions are atomic (i.e. provide an “all-or-nothing” proposition):"

`Read Uncommitted` is the MongoDB's default isolation level. [source](https://docs.mongodb.com/manual/core/read-isolation-consistency-recency/)

  **Multi-document transaction:**
```javascript
Session.startTransaction(<options>) // BEGIN
Session.abortTransaction()          // ROLL BACK
Session.commitTransaction()         // COMMIT
```

[startTransaction(), source](https://docs.mongodb.com/manual/reference/method/Session.startTransaction/)

#### 53) How do indexes support the efficient execution of queries in MongoDB? What are the consequences of adding an index in MongoDB?
[ref](https://docs.mongodb.com/manual/indexes/)  
Indexes support the efficient execution of queries in MongoDB. Without indexes, MongoDB must perform a collection scan, i.e. scan every document in a collection, to select those documents that match the query statement. If an appropriate index exists for a query, MongoDB can use the index to limit the number of documents it must inspect.

#### 54) Which index is unique and prevents clients from inserting two documents with the same value for the \_id field?
Unique index.  
the \_id index

#### 55) Which index type provided by MongoDB supports searching for string content in a collection: string, text or char?

tExT (At most one text indexing for a collection)



MongoDB supports `Text` indexing. This makes it possible to search for words in a text.

It tokenize all the words in the search string, which results in `['java', 'coffee', 'shop']`.
  
```javascript
db.stores.find( { $text: { $search: "java coffee shop" } } )
```

[source](https://docs.mongodb.com/manual/core/index-text/)

#### 56) Can MongoDB return sorted results by using the ordering in the index?
https://docs.mongodb.com/manual/tutorial/sort-results-with-indexes/
Yes, you can specify the sorting order when creating an index. An ascending index on a field named age would look like this:  
`db.records.createIndex( { age: 1 } )`  
For descending it would look like this:  
`db.records.createIndex( { age: -1 } )`
Indexes are special data structures that store a small portion of the collection’s data set in an easy to traverse form.

#### 57) Which operation adds a new document to the user’s collection?

```javascript
db.collection.insert({...})//depricated from 4.2
db.collection.insertOne({...})
db.collection.insertMany({...})
```

#### 58) Which operator is similar to ORDER BY clause in RDBMS?

db.collection.find().sort({...})

In addition you can aslo use the *$orderby* n 

#### 59) How can you limit the number of documents in result set? How is COUNT function provided in MongoDB?

By using the `limit` functions.
  
```javascript
db.collection.find(OPTIONS).limit(AMOUNT)
```
  
By using the `count` functions.
  
```javascript
db.collection.find(OPTIONS).count()
```
Count can be used inside aggregate functions:  
```javascript
db.collection.aggregate( [
   { $count: "myCount" }
])
```

#### 60) What are the strengths and weaknesses of MongoDB? When is MongoDB the best choice of database type and when it should be avoided? Name some typical use cases and applications.

Pros:
- Flexible schema  
- Horizontal scaling (Sharding)
- MapReduce/aggregate functions
- JAVASCRIPT
- Michael er fan (y)
- Good for simple-minded-people  .....
- A good first database to learn, before you learn a real one

Cons:
- JAVASCRIPT
- DUBLICATE DATA XD NICE DB

Use cases:
- Logging
- historic data
- archive documents
- content management

### Graph-Oriented Database  

#### 61) What type of database Neo4j is? Which data model it is built on? How does it differ from the relational model? Which types of operations with data does it support?

https://neo4j.com/developer/guide-data-modeling/#:~:text=A%20Neo4j%20graph%20data%20model,structure%20for%20the%20graph%20database.
Neo4j is a graph database. 

Data stored on disk is all linked lists of fixed size records. Properties are stored as a linked list of property records, each holding a key and value and pointing to the next property. Each node and relationship references its first property record. The Nodes also reference the first relationship in its relationship chain. Each Relationship references its start and end node. It also references the previous and next relationship record for the start and end node respectively. [source](https://neo4j.com/developer/kb/understanding-data-on-disk/)

Rather than making relationships between SQL relations(tables), you make relationships between the individual rows/nodes.  
Furthermore, you can label the relationships and add properties to them in Neo4j.  

It supports a variety of graph algorithms such as:  
- Centrality algorithms
- Community detection algorithms
- Similarity algorithms
- Path finding algorithms
- Link Prediction algorithms
- Auxiliary procedures
https://neo4j.com/docs/graph-data-science/current/algorithms/

#### 62) Which is the underlying storage model of Neo4j database? Which advantages does it provide?

Data stored on disk is all linked lists of fixed size records. Properties are stored as a linked list of property records, each holding a key and value and pointing to the next property. Each node and relationship references its first property record. The Nodes also reference the first relationship in its relationship chain. Each Relationship references its start and end node. It also references the previous and next relationship record for the start and end node respectively. [source](https://neo4j.com/developer/kb/understanding-data-on-disk/)

Because of this chaining structure, the notion of traversal (i.e. THE way of querying data) easily emerges. That's why a graph database like Neo4j excels at traversing graph-structured data.

#### 63) Which are the components of Neo4j development platform? Which connectivity methods are available? Which are the main libraries, extending the core functionality of Neo4j?

* APOC
* GDSL (Graph data science library)
* Graph algorithms 
  
https://neo4j.com/developer/graph-platform/
* Neo4j Graph Database – our core graph database that is built to store and retrieve connected data. There are two editions – a Community Edition and an Enterprise Edition. Everything in our platform interacts with data stored in the database.
* Neo4j Desktop – application to manage local instances of Neo4j. Free download includes Neo4j Enterprise Edition license.
* Neo4j Browser – online browser interface to query and view the data in the database. Basic visualization capabilities using Cypher query language.
* Neo4j Bloom – visualization tool for business users that does not require any code or programming skills to view and analyze data. Documentation is also available in our docs section.  

Neo4j provides a REST API which you can call cypher commands via. the REST protocols.  
You can connect via. HTTP, HTTPS, BOLT.
[source](https://hackmd.io/DIcqpBcWQzOpMqNWQHfP3A?both) FIX LINK

#### 64) How does Neo4j respond to ACID and CAP? How does clustering relate to ACID and CAP features? Which cluster architectures are available for Neo4j?

CA (Not partition tolerant?) (AP if you ask book)

![](https://i.imgur.com/ZD5C3iz.png)


[Neo4j is fully ACID-compliant](https://www.graphgrid.com/neo4j-is-designed-to-be-your-source-of-truth-database/#:~:text=But%20it's%20a%20fact%3A%20Neo4j,truth%20database%20for%20your%20enterprise.&text=Neo4j%20ensures%20that%20operations%20involving,transaction%20to%20guarantee%20consistent%20data.)  


Neo4j HA is recommended for read-mostly requirements.

Up until neo4j 3.5 you had causal and HA (High Availability) cluster architectures. However HA has been deprecated ([link](https://neo4j.com/developer/kb/comparing-ha-vs-causal-clusters/)), and now you should only implement casual cluster architecture. This consists of core servers you can read write to, and then replica servers which you can only read from

![](https://i.imgur.com/y8GjCzB.png)

#### 65) How does Neo4j support transactions and indexing? How do read and write operations differ when executed in a cluster?

While it is not possible to run a Cypher query outside a transaction, it is possible to run multiple queries within a single transaction using the following sequence of operations:  
1. Open a transaction,
2. Run multiple updating Cypher queries.
3. Commit all of them in one go.
https://neo4j.com/docs/cypher-manual/current/administration/indexes-for-search-performance/
Index:  
```c
CREATE INDEX [index_name]
FOR (n:LabelName)
ON (n.propertyName)
```  
**Causal clusters:**  
**Writes:**  
A Neo4j cluster consists of Core Servers (Read/write) and Read Replicas.  
When you write to a core server, the write wil be acknowledged by thge fastest majority of core servers. As the number of core servers in the cluster grows, so do the size of the majority needed to acknowledge the write.  
**Reads:**  
Read Replicas are asynchronously replicated from Core Servers.They will periodically poll an upstream server for new transactions and have these shipped over. Many Read Replicas can be fed data from a relatively small number of Core Servers, allowing for a large fan out of the query workload for scale.  


Extra til clustering:  
A clean Core Server shutdown, like Core Server booting, is handled via the Raft protocol. When a Core Server is shut down, it appends a membership entry to the Raft log which is then replicated around the Core Servers. Once a majority of Core Servers have committed that membership entry the leaver has logically left the cluster and can safely shut down. All remaining instances accept that the cluster has grown smaller, and is therefore less fault tolerant. If the leaver happened to be playing the Leader role at the point of leaving, it will be transitioned to another Core Server after a brief election.

An unclean shutdown does not directly inform the cluster that a Core Server has left. Instead the Core cluster size remains the same for purposes of computing majorities for commits. Thus an unclean shutdown in a cluster of 5 Core Servers now requires 3/4 members to agree to commit which is a tighter margin than 3/5 before the unclean shutdown.

* Of course when Core Servers fail, operators or monitoring scripts can be alerted so that they can intervene in the cluster if necessary.

If the leaver was playing the Leader role, there will be a brief election to produce a new Leader. Once the new Leader is established, the Core cluster continues albeit with less redundancy. However even with this failure, a Core cluster of 5 servers reduced to 4 can still tolerate one more fault before becoming read-only.

#### 66) Which query language is used for processing the graph data? Which are the objects It operates with?
Cypher

Nodes/relationships  
DB management (Creating indexes, users etc.)

#### 67) Which categories of graph algorithms are enabled in Neo4j? What is their implementation? Give some examples of algorithms in each category. Give some examples of business cases, which benefit from the implementation of graph algorithms.

- Centrality algorithms:
This is to score nodes based on how "popular" they are. This can be defined by its relation and how popular those individual relations are
    - Page rank
- Community detection algorithms
Community detection algorithms are used to evaluate how groups of nodes are clustered or partitioned, as well as their tendency to strengthen or break apart.
	- Louvain
	- Label Propagation
	- Weakly Connected Components
	- Triangle Count
	- Local Clustering Coefficient
- Similarity algorithms
Similarity algorithms compute the similarity of pairs of nodes using different vector-based metrics.
    - Node Similarity
- Path finding algorithms
Finds the shortest path between two or more nodes
**Used fx. for GPS**
    - A*, Shortest Path, Minimum Weight Spanning Tree.
- Link Prediction algorithms
Link prediction algorithms help determine the closeness of a pair of nodes. The computed scores can then be used to predict new relationships between them
    - Adamic Adar
    - Common Neighbors
    - Preferential Attachment
    - Resource Allocation
    - Same Community
    - Total Neighbors

#### 68) What are the strengths and weaknesses of Neo4j? When is Neo4j the best choice of database type and when it should be avoided? Name some typical use cases and applications.

**Strengths**  
Neo4j has a high performance on deeply connected queries. This is because the database only will check the part that traversed by the query instead on the whole graph.

Transition from sketch to structures is almost seamless.

Good for object or network like structures.

Is compliant with ACID and provides full transaction support. And of cource easy to learn.

**Weaknesses**  
The cluster only has a few write servers. This means neo4j doesn't scale write operations that well. Only vertical scaling is possible on the core server.

Neo4j has a limit for storage. This limit is super high so normal humans dont need to worry, only businesses like Google can exide it.

No date type, which means date shall be represented as strings or unix time.

**Use Cases**  
Use cases for this type of database is hugh. Every social network should base the data on this type og database, because of the easy way to make data out of data. Page Rank would be an example here.

Medicine where diseases, symptoms, medicine and doctors are connected.

Artificial intelligence, where patterns can be used to predict future outcomes.

etc.

best use cases
- Machine Learning
- Fraud Detection
- Regulatory Compliance
- Supply Chain Transparency

### Key-Value Data Store

#### 69. What type of database is Redis? Which data model does it use? How does it differ from RDB?

Redis is an in-memory key-value database. It support data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, geospatial indexes with radius queries and streams. In relational databases, data is stored in columns and tables. For Redis, data is stored as key value pairs.  
    Compared to RDB Redis is much faster at read/write operations.  
    You can' store as much data with Redis as you can with RDB, as RDB uses secondary memory and has a much bigger capacity.  
    RDBS allows for more complicated queries compared to Redis.
    
#### 70. Explain the Replication feature of Redis?

[redis blog](https://redis.io/topics/replication)
The replication feature uses master-slave replication. It allows replica Redis instances to be exact copies of a master. The replica automatically reconnects to the master every time the link breaks, and will attempt to be an exact copy of it regardless of what happens to the master. When anything happens on the master it keeps the slaves updated by sending a stream of commands to the slaves.  
    When the link breaks, the slaves will try to proceed with a partial resynchronization, which means it will try to just obtain the part of the stream of commands it missed during the disconnection.  
    When a partial resync is not possible, the replica will ask for full resync. The master will then create a snapshot of all of it's data, and send it to the replica, and then it will continue streaming commands.

#### 71. List out the operation keys of Redis.

-   Set - Store a single value on a key
-   HSET - Sets a string value on a hash field
-   MGET - Return values of all specified keys.
-   HMSET - Sets multiple hash fields to multiple values
-   INCR - Increment a integer value on a key by one
-   INCRBY - Increment an integer value on a key by x
-   EXPIRE - Sets a key's time to live in seconds
-   DEL - Deletes a key
-   MULTI - Mark the start of a transaction block
-   EXEC - Execute all commands issued after MULTI

#### 72. Does Redis give speed and durability both?

No.  
    Redis does support durability with Snapshots, and Append-Only File.  
    Append-Only File: Every shard of a Redis database appends new lines to its persistent file either every second(fast but less safe as you can lose a second worth of data) or every write (safer but slower).  
    AOF is safe from corruption since it is append only, and if a line is half written, they have a tool that can reasily fix it (redis-check-aof).  
    When the AOF log is too big, Redis can automatically rewrite it in the background, this is completely safe and Redis continues to append ot the old file, a new one is produced with the minimal set of operations needed to create the current data set. When the new filed is ready, Redis switches the two and start appending to the new one.  
    The file contains a log of all operations one after the other.  
    Compared to Snapshots, the AOF is typically bigger for the same dataset. It can be slower than snapshots if it saves after every query.  
    Snapshots allow for data durability, they write the entire point-in-time view of the dataset to persistent storage, across all shards of the database. This allows you to recover data in case of disasters. However, this you will lose data which was stored inbetween the disaster and the last snapshot. Snapshots need to call fork() often in order to persist on disk using a child process. This call can be time consuming on large datassets, and may result in Redis stopping from working for some ms or even for one second.  
    The only way to have full durability, would be to use the AOF write after every query feature, but it slows down Redis.
    
#### 73. How can you improve the durability in Redis?

You can combine AOF and Snapshots in the same instance. When Redis restarts the AOF file will be used to reconstruct the OG dataset, since it is guaranteed to be the most complete. Snapshots are faster for restarts and there can be bugs in the AOF engine.

#### 74. Mention what are the things you have to take care while using Redis?

Storage is limited.  
RAM is volatile, so you can consider setting up an AOF (append only file or a snapshot)

#### 75. What are the strengths and weaknesses of Redis? When is Redis the best choice of database type and when it should be avoided? Name some typical use cases and applications.

**Strengths:**  
     Redis performes read and write operation incredibly fast as it uses the RAM.
    It supports complex data structures such as lists, hashes sets and sorted sets.  
     It is highly available with the master-slave system called Redis Sentinel.  
     It supports on disk persistance (AOF, Snapshots).  
     Built-in replication and automatic sharding. [ref](https://redis.io/topics/partitioning)  
     Single-threaded with transaction support.
     You can set data to expire after a certain time.
     
**Weaknesses:**  
    Storage is limited by memory.  
    Depending on your config of append only file (append every second, append every query), taking snapshots can slow the database down.  
    It is difficult to model relationships.  
    No aggregate functions such as sum/acerage, they need to be done client side.  
    Indexing isn't supported internally but can use Sets as workaround.  
    No support for any query language.  
    Redis only supports basic password security.
    Redis is best used for smaller datasets where relation between the data it stores is irrellevant. Redis is also good if you need a lot of speed but not a lot of storage.  
    It is ideal for applications such as session information, shopping carts or even a chat server.
