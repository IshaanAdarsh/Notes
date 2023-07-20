# MongoDB

## Installation:
- [MongoDB-community](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/#installing-mongodb-6.0-edition-edition)
- [mongosh (MongoDB Shell)](https://www.mongodb.com/docs/mongodb-shell/install/#std-label-mdb-shell-install)

MongoDB Structure:
Documents live in collections and collections live inside of Databases
```
- Database
  - Collection 1
    - Document 1
    - Document 2
    - Document 3
```
## Basic Commands:
### show dbs:
- Show all databases in the current MongoDB instance
```js
test> show dbs
admin   40.00 KiB
config  12.00 KiB
local   72.00 KiB
```
### use <database>:
- Created a new database with that name or connects to the same-named database
```js
test> use appdb
switched to db appdb
```

### show collections:
-  In MongoDB you have 2 types of data:
  - Databases
  - Collections: Tables inside of the Database
```js
appdb> show collections
users
```

### cls:
- Clears the screen/shell.

### exit:
- Closes the mongosh and exits the shell

### db.dropDatabase():
- Use this to drop a database (kind of like a js function)
```js
appdb> db.dropDatabase()
{ ok: 1, dropped: 'appdb' }
appdb>
```
-  Something amazing about MongoDB is that we are still in the database appdb, this is because if something doesn't exist in MongoDB and you try to put data in it the server creates that database or collection automatically.

## Insert Commands:
### insertOne:
- Create a new document inside the specified collection
- MongoDB already makes a private key (_id) for the element inserted into the collection
```js
//simple
appdb> db.users.insertOne({name: "John"})                  // JSON object
{
  acknowledged: true,
  insertedId: ObjectId("64b8c006d0be38f4602e20b1")
}

// As there is no schema, you can add how many things in the collection
appdb> db.users.insertOne({name: "Sally", age: 19, address: {street: "987 North St"}, hobbies: ["Running"]})
{
  acknowledged: true,
  insertedId: ObjectId("64b8c212d0be38f4602e20b2")
}
```

### find:
- Shows the number of entries in the document.
```js
// Simple
appdb> db.users.find()
[ { _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' } ]

//Complex
appdb> db.users.find()
[
  { _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' },
  {
    _id: ObjectId("64b8c212d0be38f4602e20b2"),
    name: 'Sally',
    age: 19,
    address: { street: '987 North St' },
    hobbies: [ 'Running' ]
  }
]
```

### insertMany:
- Create multi new documents inside a specific collection
```js
appdb> db.users.insertMany([{ age: 26 }, { age: 20 }])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("64b8c348d0be38f4602e20b3"),
    '1': ObjectId("64b8c348d0be38f4602e20b4")
  }
}

appdb> db.users.find()
[
  { _id: ObjectId("64b8c348d0be38f4602e20b3"), age: 26 },
  { _id: ObjectId("64b8c348d0be38f4602e20b4"), age: 20 }
]
```

## Basic Query Commands (Read and Read Modifiers):
### find variations:
- **find()**
  - Get all Documents if params not specified
```js
appdb> db.users.find()
[
  { _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' },
  {
    _id: ObjectId("64b8c212d0be38f4602e20b2"),
    name: 'Sally',
    age: 19,
    address: { street: '987 North St' },
    hobbies: [ 'Running' ]
  },
  { _id: ObjectId("64b8c348d0be38f4602e20b3"), age: 26 },
  { _id: ObjectId("64b8c348d0be38f4602e20b4"), age: 20 }
]

appdb> db.users.find({name: "Sally"})                      // Paramaeter is specified
[
  {
    _id: ObjectId("64b8c212d0be38f4602e20b2"),
    name: 'Sally',
    age: 19,
    address: { street: '987 North St' },
    hobbies: [ 'Running' ]
  }
]
```

- **find(<filterObject>)**
  - Find all documents that match the filter object
```js
appdb> db.users.find({ name: "John"})
[ { _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' } ]                // Just returns document with the name John
```

- **find(<filterObject>, <selectObject>)**
  - Find all documents that match the filter object but only return the field specified in the select object
```js
appdb> db.users.find({ name: "Sally" }, { name: 1, age: 1 })              // 1 - Show
[                                                                         // 0 - Hide
  { _id: ObjectId("64b8c212d0be38f4602e20b2"), name: 'Sally', age: 19 }
]

appdb> db.users.find({ name: "Sally" }, { name: 1, age: 1 , _id: 0})
[ { name: 'Sally', age: 19 } ]
```

- **findOne**
  - Returns only the first document which matches the object
```js
appdb> db.users.findOne({ name: "John" })
{ _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' }
```

### count:
- **countDocuments**
  - Return the count of the documents that match the filter object passed to it
```js
appdb> db.users.countDocuments({ name: "John"})
1
```

### Sort:
- Sort the results of a find by the given fields (mat hed the first field and then the next)
```js
// sort -> 1 = increasing
// sort -> -1 = decreasing

appdb> db.users.find().sort({ name: 1, age: -1 })
[
  { _id: ObjectId("64b8c348d0be38f4602e20b3"), age: 26 },
  { _id: ObjectId("64b8c348d0be38f4602e20b4"), age: 20 },
  { _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' },
  {
    _id: ObjectId("64b8c212d0be38f4602e20b2"),
    name: 'Sally',
    age: 19,
    address: { street: '987 North St' },
    hobbies: [ 'Running' ]
  }
]
```

### limit:
- Only returns a set number of documents
```js
appdb> db.users.find().limit(2)
[
  { _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' },
  {
    _id: ObjectId("64b8c212d0be38f4602e20b2"),
    name: 'Sally',
    age: 19,
    address: { street: '987 North St' },
    hobbies: [ 'Running' ]
  }
]
```

### skip:
- Skips a set number of documents form the beginning
```js
appdb> db.users.find().skip(1)                                // Skips John
[
  {
    _id: ObjectId("64b8c212d0be38f4602e20b2"),
    name: 'Sally',
    age: 19,
    address: { street: '987 North St' },
    hobbies: [ 'Running' ]
  },
  { _id: ObjectId("64b8c348d0be38f4602e20b3"), age: 26 },
  { _id: ObjectId("64b8c348d0be38f4602e20b4"), age: 20 }
]
```
## Complex Query Commands:
### $eq:
- Check for equality
```js
appdb> db.users.find({ name: { $eq: "Sally" } })            // Get all the users with the name Sally
[
  {
    _id: ObjectId("64b8c212d0be38f4602e20b2"),
    name: 'Sally',
    age: 19,
    address: { street: '987 North St' },
    hobbies: [ 'Running' ]
  }
]
```

### $ne:
- Check for not equal
```js
appdb> db.users.find({ name: { $ne: "Sally" } })                    // Get all users with a name other than Sally
[
  { _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' },
  { _id: ObjectId("64b8c348d0be38f4602e20b3"), age: 26 },
  { _id: ObjectId("64b8c348d0be38f4602e20b4"), age: 20 }
]
```

### $gt / $gte:
- Check for greater than ($gt) and greater than or equal ($gte) to
```js
appdb> db.users.find({ age: { $gt: 20 } })
[ { _id: ObjectId("64b8c348d0be38f4602e20b3"), age: 26 } ]

appdb> db.users.find({ age: { $gte: 20 } })
[
  { _id: ObjectId("64b8c348d0be38f4602e20b3"), age: 26 },
  { _id: ObjectId("64b8c348d0be38f4602e20b4"), age: 20 }
]
```

### $lt / $lte:
- Check for less than ($lt) and less than or equal ($lte) to
```js
appdb> db.users.find({ age: { $lt: 20 } })
[
  {
    _id: ObjectId("64b8c212d0be38f4602e20b2"),
    name: 'Sally',
    age: 19,
    address: { street: '987 North St' },
    hobbies: [ 'Running' ]
  }
]

appdb> db.users.find({ age: { $lte: 20 } })
[
  {
    _id: ObjectId("64b8c212d0be38f4602e20b2"),
    name: 'Sally',
    age: 19,
    address: { street: '987 North St' },
    hobbies: [ 'Running' ]
  },
  { _id: ObjectId("64b8c348d0be38f4602e20b4"), age: 20 }
]
```

### $in:
- Check if a value is one of many values
```js
appdb> db.users.find({ name: { $in: ["John", "Mike"] } })
[ { _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' } ]
```

### $nin:
- Check if a value is none of many values
```js
appdb> db.users.find({ name: { $nin: ["Sally", "Mike"] } })
[
  { _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' },
  { _id: ObjectId("64b8c348d0be38f4602e20b3"), age: 26 },
  { _id: ObjectId("64b8c348d0be38f4602e20b4"), age: 20 }
]
```

### $and:
- Check that multiple conditions are all true
```js
// get all users with a name of John and an age of 26
appdb> db.users.find({ $and: [{ age: 26 }, { name: "John" }] })
                                                                  \\ No values
```

### $or:
- Check that one of multiple conditions is true
```js
// get all users with a name of John or an age of 26
appdb> db.users.find({ $or: [{ age: 26 }, { name: "John" }] })
[
  { _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' },
  { _id: ObjectId("64b8c348d0be38f4602e20b3"), age: 26 }
]
```

### $not:
- Negate the filter inside of $not
```js
// Get all the users with a name other than John
appdb> db.users.find({ name: { $not: { $eq: "John" } } })
[
  {
    _id: ObjectId("64b8c212d0be38f4602e20b2"),
    name: 'Sally',
    age: 19,
    address: { street: '987 North St' },
    hobbies: [ 'Running' ]
  },
  { _id: ObjectId("64b8c348d0be38f4602e20b3"), age: 26 },
  { _id: ObjectId("64b8c348d0be38f4602e20b4"), age: 20 }
]
```

### $exists:
- Check if a field exists
```js
// Get all users that have a name field
appdb> db.users.find({ name: { $exists: true } })
[
  { _id: ObjectId("64b8c006d0be38f4602e20b1"), name: 'John' },
  {
    _id: ObjectId("64b8c212d0be38f4602e20b2"),
    name: 'Sally',
    age: 19,
    address: { street: '987 North St' },
    hobbies: [ 'Running' ]
  }
]
```

### $expr:
- Do comparisons between different fields
```js
// Get all users that have a balance that is greater than their debt
appdb> db.users.find({ $expr: { $gt: [“$balance”, “$debt”] } })

```

## Update:
### updateOne:
- Update the first document that matches the filter object with the data passed into the second parameter which is the update object.
```js
// Update the first user with an age of 20 to the age of 21
appdb> db.users.updateOne({ age: 20 }, { $set: { age: 21 } })
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```

### updateMany:
- Update all documents that matches the filter object with the data passed into the second parameter which is the update object.
```js
// Update all users with an age of 12 by adding 3 to their age
appdb> db.users.updateMany({ age: 26 }, { $inc: { age: 3 } })
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```

### replaceOne:
- Replace the first document that matches the filter object with the exact object passed as the second parameter. This will completely overwrite the entire object and not just update individual fields.
```js
// Replace the first user with an age of 3 with an object that has the age of 13 as its only field
appdb> db.users.replaceOne({ age: 3 }, { age: 13 })
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
```




