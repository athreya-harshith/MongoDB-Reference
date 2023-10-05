## MongoDb Reference
* **__DATA BASE__** : Data Can be stored in different ways , similar to traditional method (files) , databases is also a way to store data.
## Relational DataBases
* These type of databases , uses tables and information retrieval involves usage of **SQL** and information is stored in form of tables.
* Some Databases that are Relational are :
  * MySql
  * PgSql ..
## NoSQL 
* NoSQL stores data in a non-relational model.
* It doesnot use tables to store data , rather it can be any of the following ones:
    * **Graph Based** 
    * **Key-Value** (Reddis)
    * **Document Based** (MongoDb)
## MongoDb
* MongoDb stores an instance of data in the Document format.
* MongoDb stores one instance of recored as document.
* Group of documents belongs to a collection.
    * Document == row/tuple
    * Collections == tables
* Every document can posses its own structure and fields.

## Features of MongoDb
* Cross platform (Independent of OS)
* Open Source
* NoSQL 
* Document Based DB
* Highly Scalable DB as it has distributed architecture
* High Performance
* Flexible
* Well Suited For wide use cases
* Query language used here is easy
* Good to handle Unstructured data
* Cloud Platform support
---
> Relational Databases are preferred to have vertical scaling and NoSQL DataBases are preferred to have horizontal scaling.
--
## Queries With MongoDB in mongo-shell
* Usage of `mongo` command in terminal is not preffered as `mongosh` has superseeded it.
* Use `mongosh` for starting mongoshell.
---
* To show the databases , use :
```mongodb
show databases;
```
* Or can also use
```mongodb
show dbs;
```
---
* To create a new database use :
```
use <db-name>;
```
* The above command creates a new database . It wont enlist it utill the created DB has atleast one collection.
---
**DEALING WITH COLLECTIONS**
* To create a new collection , use :
```
db.createCollection("collectionName");
```
* This creates a new collection with the name given , and it give the following as a result.
```
{ ok: 1 }
```
* To Enlist all the documents within a collection , use :
```
db.collectionName.find();
```
* To Insert a single data into a collection,
```
db.courses.insertOne({name:"Physics",type:"Practical",marks:100});
```
* To insert multiple data into a collection,
```
db.courses.insertMany([{name:"English",type:"Theory"},{name:"P.Ed",mandatory:"NO"}]);
```
* **FILTERS**
* To find the first document inside a collection , 
```
db.courses.findOne();
```
* To find all the document inside a collection,
```
db.courses.find();
```
* To find a document with some condition , 
```
db.courses.find({ type: 'Practical' });
```
* To find the first document with some condition , 
```
db.courses.findOne({ type: 'Practical' });
```
* To find the document with an id , 
```
db.courses.find(ObjectId('651e2eb9e41d11ce0060bf66'))
```
* Or it can also be retrieved by 
```
db.courses.find({_id:ObjectId('651e2eb9e41d11ce0060bf66')});
```



