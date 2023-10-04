#MongoDB Cheat Sheet

First steps in the MongoDB World? This cheat sheet is filled with some handy tips, commands, and
quick references to get you connected and CRUD'ing in no time!

##Table of Contents

- [Connect Via `Mongosh`](#connect-via-mongosh)
- [Helpers](#helpers)
  - [Show Databases](#show-databases)
  - [Switch Database](#switch-database)
  - [Show Collections](#show-collections)
- [Database and Collections](#database-and-collections)
  - [Drop](#drop)
  - [Run Javascript File](#run-javascript-file)
- [CRUD](#crud)
  - [Create / Insert](#create--insert)
  - [Read / View](#read--view)
  - [Update](#update)
  - [Delete/Remove](#deleteremove)
- [MongoDB Operators](#mongodb-operators)
  - [Query and Projection Operators](#query-and-projection-operators)
  - [Update Operations Operator](#update-operations-operator)

#### Connect Via `Mongosh`

```
mongosh # connects to mongodb://127.0.0.1:27017 by default
mongosh --host <host> --port <port> --authenticationDatabase admin -u <user> -p <pwd> # omit the password if you want a prompt
mongosh "mongodb://<user>:<password>@192.168.1.1:27017"
mongosh "mongodb://192.168.1.1:27017"
mongosh "mongodb+srv://cluster-name.abcde.mongodb.net/<dbname>" --apiVersion 1 --username <username> # MongoDB Atlas
```

#### Helpers

##### Show Databases

```shell
show dbs
db // prints the current database
```

##### Switch Database

```Shell
 use <databaseName> //use mydb
```

##### Show Collections

```Shell
show collections
```

#### Database and Collections

##### Drop

```shell
db.<collectionName>.drop() // drop the collection
db.dropDatabase()   // drop the database
```

##### Run Javascript File

```Shell
load("myScript.js")
```

#### CRUD

##### Create / Insert

```javascript
db.<collectionName>.insertOne()
//Insert one object data into the collection

db.<collectionName>.insertMany()
 //Insert many objects data into the collection as Array of objects

db.<collectionName>.insertMany([{name:"devripon"},{name: "Alex"},{ordered : false}])
 //Insert many objects data into the collection as Array of objects with Unordered

db.<collectionName>.insertOne({date : ISODate()})
 //insert ISO date into the collection
```

##### Read / View

```javascript

    db.<collectionName>.find();
     //Find all objects. it will return 20 data in a page

    db.<collectionName>.findOne();
     //return a single object in the collection

    db.<collectionName>.find().pretty();
     // return all objects in the collection as Prettier formate

    db.<collectionName>.find({name: "devripon",age:30})
     // It will return data logically in the collection by using Implicit Logical `&&` operator

    db.<collectionName>.find({name: "devripon"})
    // search data in the collection by using Object Query

    db.<collectionName>.find({date:ISODate("2023-10-04T07:11:34.113Z")
     // return data by using date query

    db.<collectionName>.distinct("name")
    // it will return all values of name key in the collection

    db.<collectionName>.find({name: "Max", age: 32}).explain("executionStats")
    // it will return data with all execution stats in details


    //Count the number of data in the collection

    db.<collectionName>.countDocuments()
    // it will return the number of documents available in the collection

    db.<collectionName>.estimatedDocuments()
     // it will return the number of documents available in the collection

    db.<collectionName>.countDocuments({name: "devripon"})
    // it will return the number of documents available in the collection of specific object queries


    // find data by comparison

    db.<collectionName>.find({"year":{$gt: 1990}})
    //it return all the data which year value is GRATER THAN 1990

    db.<collectionName>.find({"year":{$gte: 1990}})
    // it return all the data which year value is GRATER THAN and EQUAL of 1990

    db.<collectionName>.find({"year":{$lt: 1990}})
    // it return all the data which year value is LESS THAN 1990

    db.<collectionName>.find({"year":{$lte: 1990}})
    // it return all the data which year value is LESS THAN and EQUAL of 1990

    db.<collectionName>.find({"year":{$ne: 1990}})
     // it return all the data which year value is NOT EQUAL of 1990

    db.<collectionName>.find({"year":{$in:[1990,1995]}})
     //it will return all the data which year value is EITHER 1990 or 1995

    db.<collectionName>.find({"year":{$nin:[1990,1995]}})
     // it will return all the data which year value is NOT 1990 OR 1995

    //Data find logically

    db.<collectionName>.find({name:{$not:{$eq: "devripon"}}})
     // it will return all the data which name value is not equal to "devripon"

    db.<collectionName>.find({$or:[{year:{$lt: 1999}},{year: {$gt: 1970}}]})
     // it will return all the data by matching anyone of those two statements

    db.<collectionName>.find({$nor:[{year:1995},{year:1990}]})
     // it will return all the data which will not match both those two statements

    db.<collectionName>.find({$and:[{year:1995},{year:1987}]})
     // it will return all the data which will match both those two statements


```

##### Update

```javascript

```

##### Delete/Remove

#### MongoDB Operators

##### Query and Projection Operators

| Oerators                       | Full Meaning                                                                                                                   |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| <strong>Comparison Operator    | <strong>This operators are used to compare of different BSON type values</strong>                                              |
| `$eq`                          | Matches values that are equal to a specified value.                                                                            |
| `$gt`                          | Matches values that are greater than a specified value                                                                         |
| `$gte`                         | Matches values that are greater than or equal to a specified value                                                             |
| `$lt`                          | Matches values that are less than a specified value                                                                            |
| `$lte`                         | Matches values that are less than or equal to a specified value                                                                |
| `$ne`                          | Matches values that are not equal to a specified value                                                                         |
| `$in`                          | Matches any of the values specified in an array.                                                                               |
| `$nin`                         | Matches none any of the values specified in an array.                                                                          |
| <strong>Logical Operator       | <strong>This operators are used for Logical operation in between different BSON type values</strong>                           |
| `$and`                         | Joins query statements with a logical `AND &&` returns all documents that match the conditions of both clauses.                |
| `$or`                          | Joins query statements with a logical `OR \|\|` returns all documents that match the conditions of either clause.              |
| `$not`                         | Inverts the effect same as logical `! NOT` of a query expression and returns documents that do not match the query expression. |
| `$nor`                         | Joins query statements with a logical NOR that returns all documents that fail to match both statements.                       |
| <strong> Element Operator      | <strong>This operators are used for find or check different BSON type values</strong>                                          |
| `$exists`                      | Matches documents that have the specified field.                                                                               |
| `$type`                        | Selects documents if a field is of the specified type.                                                                         |
| <strong>Evaluation Operator    | <strong>This operators are used for evaluate in different BSON type data</strong>                                              |
| `$expr`                        | Allows use of aggregation expressions within the query language.                                                               |
| `$jsonSchema`                  | Allows to Validate documents against the given JSON Schema.                                                                    |
| `$mod`                         | Performs a modulo operation on the value of a field and selects documents with a specified result.                             |
| `$regex`                       | Selects documents where values match a specified regular expression.                                                           |
| `$text`                        | Performs text search.                                                                                                          |
| `$where`                       | Matches documents that satisfy a JavaScript expression.                                                                        |
| <strong>Array Operator         | <strong>This operators are used for evaluate in different BSON type data</strong>                                              |
| `$all`                         | Matches arrays that contain all elements specified in the query.                                                               |
| `$elemMatch`                   | Selects documents if element in the array field matches all the specified `$elemMatch` conditions                              |
| `$size`                        | Selects documents if the array field is a specified size.                                                                      |
| <strong>Projection Operator    | <strong>This operators are used for projection in different BSON type data</strong>                                            |
| `$`                            | Projects the first element in an array that matches the query condition.                                                       |
| `$meta`                        | Projects the document's score assigned during `$text` operation.                                                               |
| `$slice`                       | Limits the number of elements projected from an array. Supports skip and limit slices.                                         |
| <strong>Miscellaneous Operator | <strong>This operators are used for evaluate in different BSON type data</strong>                                              |
| `$comment`                     | Adds a comment to a query predicate.                                                                                           |
| `$rand`                        | Generates a random floating point numbers between 0 and 1.                                                                     |

##### Update Operations Operator

| <strong>Fields Update Operator | <strong>This operators are used for update Fields</strong>                                                                                    |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `$correntDate`                 | Sets the value of a field to current date, either as a Date or a Timestamp.                                                                   |
| `$inc`                         | Increments the value of the field by the specified amount.                                                                                    |
| `$min`                         | Only updates the field if the specified value is less than the existing field value.                                                          |
| `$max`                         | Only updates the field if the specified value is greater than the existing field value                                                        |
| `$mul`                         | Multiplies thevalue of the field by the specified amount.                                                                                     |
| `$rename`                      | Renames a field                                                                                                                               |
| `$set`                         | Sets the value of a field in a document.                                                                                                      |
| `$setOnInsert`                 | Sets the value of a field if an update results in an insert of a document. Has no effect on update operations that modify existing documents. |
|                                |
| `$unset`                       | Removes the specified field from a document.                                                                                                  |
| <strong>Array Update Operator  | <strong>This operators are used for update Array data</strong>                                                                                |
| `$`                            | Acts as a placeholder to update the first element that matches the query condition.                                                           |
| `$[]`                          | Acts as a placeholder to update all elements in an array for the documents that match the query condition.                                    |
| `$[<identifier>]`              | Acts as a placeholder to update all elements that match the arrayFilters condition for the documents that match the query condition.          |
| `$addToSet`                    | Adds elements to an array only if they do not already exist in the set.                                                                       |
| `$pop`                         | Removes the first or last item of an array.                                                                                                   |
| `$pull`                        | Removes all array elements that match a specified query.                                                                                      |
| `$push`                        | Adds an item to an array                                                                                                                      |
| `$pullAll`                     | Removes all matching values from an array.                                                                                                    |
| `$each`                        | Modifies the `$push` and `$addToSet` operators to append multiple items for array updates.                                                    |
| `$position`                    | Modifies the $push operator to specify the position in the array to add elements.                                                             |
| `$slice`                       | Modifies the $push operator to limit the size of updated arrays.                                                                              |
| `$sort`                        | Modifies the $push operator to reorder documents stored in an array.                                                                          |
