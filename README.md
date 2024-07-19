# These commands form the basics of managing data within MongoDB. They are fundamental for managing databases, collections, and documents in MongoDB.

## Database Commands

### show dbs

    Lists all available databases.

### use databaseName

    Switches to the specified database. Creates the database if it doesn't exist when you first insert data.

### db

    Displays the current database.

## Collection Commands

### show collections

    Lists all collections in the current database.

### db.createCollection(name, options)

     Creates a new collection

## Document Commands

### db.collectionName.insertOne(document)

    Inserts a single document into a collection.

### db.collectionName.insertMany([documents])

    Inserts multiple documents into a collection.

### db.collectionName.find()

    This fetches all documents in the collection.

### db.collectionName.find({ key: "value" })

    Find all documents where name is "Alice".

### db.collectionName.find({ key: "value" }, { field1: 1, field2: 1 })

- db.collectionName.find(): This is the method used to search for documents in a collection.
- { key: "value" }: This is the query part. It specifies the condition for which documents you want to find. In this case, it looks for documents where the field key is "value".
- { field1: 1, field2: 1 }: This is the projection part. It specifies which fields to include in the results. 1 means include that field, and 0 means exclude it.

  Imagine you have a collection called students with the following documents:

- { "\_id": 1, "name": "Alice", "age": 25, "major": "Computer Science" }
- { "\_id": 2, "name": "Bob", "age": 22, "major": "Mathematics" }
- { "\_id": 3, "name": "Alice", "age": 30, "major": "Physics" }

  If you want to find documents where name is "Alice" and only show the age and major fields, you would use:

- db.students.find({ name: "Alice" }, { age: 1, major: 1 })
  You would get:

- { "\_id": 1, "age": 25, "major": "Computer Science" }
- { "\_id": 3, "age": 30, "major": "Physics" }

  Query: name: "Alice" finds documents where the name is "Alice".
  Projection: { age: 1, major: 1 } includes only the age and major fields in the result.

### db.collection.findOne(query)

     Retrieves a single document.

### db.collection.updateOne(filter, update, options)

     Updates a single document.

### db.collection.updateMany(filter, update, options)

     Updates multiple documents.

### db.collection.replaceOne(filter, replacement)

     Replaces a document.

### db.collection.deleteOne(filter)

     Deletes a single document.

### db.collection.deleteMany(filter)

     Deletes multiple documents.

## Index Commands

### db.collection.createIndex(keys, options)

     Creates an index on a collection.

### db.collection.getIndexes()

     Lists all indexes on a collection.

Administrative Commands

### db.stats()

     Provides statistics about the current database.

### db.collection.stats()

     Provides statistics about a collection.

### db.collection.drop()

     Drops a collection.

### db.dropDatabase()

     Drops the current database.

## User Management Commands

### db.createUser(user, options)

    Creates a new user.

### db.dropUser(username)

     Removes a user from the database.
