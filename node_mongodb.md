# MongoDB and Node.js

## Setup

- Install MongoDB driver using `npm`, then require `mongodb`

## Creating a database

1. Create a MongoClient object
2. Specify a connection URL with the correct IP address and the name of the database
3. MongoDB creates the database if it doesn't exist, and makes a connection to it

- Connect using the `MongoClient.connect()` method
- Databases are not created until they get content

## Collections

- `createCollection()`: create a collection

```
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";

MongoClient.connect(url, (err, db) => {
    if (err) throw err;
    var dbo = db.db("mydb");
    dbo.createCollection("customers", (err, res) => {
        if (err) throw err;
        console.log("Collection created!");
        db.close();
    });
});
```

## Insert

- _Inserting documents into a collection that doesn't exist automatically creates the document_
- `insertOne()`: insert a **document** (record in MySQL) into a collection
  - Takes:
    1. Object with name and value for each necessary field
    2. Callback with `(err, result)`

```
var myObj = { name: "CSA", address: "Montreal" };
dbo.collection("customers").insertOne(myObj, (err, res) => {
    if(err) throw err;
    console.log("1 document inserted!");
    db.close();
});
```

- `insertMany()`: insert _many_ documents into a collection
  - Takes:
    1. _Array_ of objects
    2. Callback
- A result object is returned, `res` in the above example. Properties of interest include `insertedCount`
- If you don't specify a `_id`, MongoDB will add one for you and assign a unique id for each document

## Delete

- `deleteOne()`: delete a document that matches the query
  - If query finds more than one document, only the first occurrence is deleted
- `deleteMany()`: delete all documents that match the query

## Find

- `findOne()`: return first occurrence of data in a collection
  - Takes:
    1. Query object
    2. Callback
- `find()`: return _all_ occurrences of data in the selection
  - Takes
    1. Query object
    2. (optional) `projection` object: describes which fields to include in the result (e.g. `{ _id: 0, name: 1}` will return only the name)
    3. Callback
- Using no parameters for either of these methods matches everything in the collection

### Query / filter

- First argument of `find()`
  - Basically just an object with fields that must be matched in returned objects
- Can also filter using **regex expressions**

## Soft

- `sort()`: sort result in ascending or descending order
  - Takes
    1. Object defining the sorting order (e.g. `{ name: 1 }` means sort by name in ascending order--use `-1` for descending)

## Drop

- `myCollection.drop((err, res) => {})` deletes a collection
  - res is a boolean indicating the success of the drop
- `dropCollection(myColl, (err, res) => {})` is the same

## Update

- `updateOne()`: update a document
  - Takes:
    1. Query object
    2. Object defining the new values of the document
    3. Callback

```
  var myquery = { address: "Valley 345" };
  var newvalues = { $set: { address: "Canyon 123" } };
  dbo.collection("customers").updateOne(myquery, newvalues, (err, res) => {})
```

- `$set` operator ensures only specified fields are updated
- `updateMany()`: update many documents

## Limit

- `limit(num)`: limit number of documents to return

## Join

- `$lookup` stage: join collections together
- MORE
