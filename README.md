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
    * **Graph Based** (Neo4j)
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
## RDBMS and NoSQL
> In **RDBMS** Data will be stored in form of tables : MySQL, MariaDB,PgSQL ...
> We use **SQL** for create , read ,write, update and deleting the records.

> NoSQL : Not Only SQL , is a category of DB which stores data in non relational fashion.
> It Doesnot use tables.
> to retrieve , insert , deleting can be done without SQL.

## MongoDB Internal Data Storage 
* `JSON` : JavaScript Object Notation
* `BSON` : Binary JSON
* MongoDB internally use BSON to store data in the disk
* It converts the data to JSON when it loads
  
## Dealing With Collections (Continued..)
* To count the number of documents inside a collection ,
```
db.collectionName.count();
```
* **LIMIT the Output in MongoDB**
```
db.collectionName.find().limit(<number>);
```
* **To select only the required attributes**
* __find()__ method takes 2 arguments , first one is the filteration criteria and the second one is the attributes to select.
* Selecting which key-value pairs as a part of result is called as **__Projection__**
```
db.collectionName.find({},{name:1,address:1});
```
* The above command selects only name and address attribute of the documents.
```
db.colllectionName.find({},{phone:0});
```
* The above command selects all the attributes except the phone.
* 0 and 1 can be interchanged with true and false.
* Example :
```
db.temp.find({_id:'10006546'},{name:1,images:1});
```
* To find the **COUNT** of matching documents ,
```
db.collectionName.find({},{}).count();
```
* Examples ,
```
db.temp.find({minimum_nights:'2'}).count();
```
```
db.temp.find({minimum_nights:'2'},{name:true}).limit(1);
```
```
db.temp.find({minimum_nights:'2'},{name:true}).limit(1).toArray();
``` 
* The below one gives **TYPE ERROR**
```
db.temp.findOne({minimum_nights:'2'},{name:true}).toArray();
```
* **ORDERING The Data**
* Ordering the data refers to arranging the result in Ascending or in Descending Order.
* To Order data , sort() method is available which takes an object as input
* key is the attribute according to which the data must be sorted 
* value can be 1 for **Ascending** and -1 for **Descending**
* Examples ,
```
db.temp.find({},{name:true,minimum_nights:true}).sort({minimum_nights:-1});
```
* If the minimum_nights value for some documents are same , the data will be sorted according the second key in the sort functions input object.
* **DELETING Document**
* To delete a document use ,
```
db.collectionName.deletOne({key:value});
```
* Example 
```
db.temp.deleteOne({_id:'19760228'});
```
 To delete **Multiple** Documents use ,
```
db.collectionName.deleteMany({key:value});
```
* Example 
```
db.temp.deleteMany({minimum_nights:'2'});
```
* ### Updating Documents
* To update the documents , we have `updateOne({<filteration-criteria>},{})` and `updateMany({<filteration-criteria>},{})` functions.
* Both the functions take 2 objects as arguments and first one is filteratio criteria , to decide what document to be updated .
* Second one uses different **operators** for different types of updations.
* `$set` this operator sets the new value for the mentioned key.
* Example ,
```
 db.data.updateOne({ _id: ObjectId("5553a998e4b02cf7151190b8")},{$set:{dataSource:'5'}});
```
* `$inc` this operator increments the key according to the given value (if value is +ve incremented and decremented if -ve).
* Example ,
```
db.data.updateOne({_id:ObjectId("5553a998e4b02cf7151190b8")},{$inc:{elevation:1}});
```
* Can also use multiple operators in one query 
```
db.data.updateOne({_id:ObjectId("5553a998e4b02cf7151190b8")},{$inc:{elevation:1},$set:{dataSource:'5'}});
```
* The response for updatOne() will be like ,
```
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```
* using updateMany() ,
```
db.data.updateMany({callLetters:'PLAT'},{$set:{elevation:10000}});
```
* The response will be like,
```
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 528,
  modifiedCount: 528,
  upsertedCount: 0
}
```
* ### Operators
* In order to provide different comparsions for the filteration criteria for a key , operators are used.
* Some operators are
  * `$ne` not equal to
  * `$lt` less than
  * `$gt` greater than
  * `$lte` less than equal to 
  * `$gte` greater than equal to
  * `$and` 
  * `$or`
  * `$in` value in some set
  * `$nin` value not in some set
* Examples ,
```
db.data.find( { callLetters: { $ne: 'PLAT' } }).count();
```
```
db.data.find({elevation:{$lt:9998}}).count();
```
* To give the range for a value , 
```
db.data.find({$and:[{elevation:{$lte:10000}},{elevation:{$gt:9999}}]}).count();
```
> To checkout what all the distinct values present for a key , we can use
> ```
db.data.distinct("key-name");
```
