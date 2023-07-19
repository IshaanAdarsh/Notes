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
- Clears the screen

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
### 
