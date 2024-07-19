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

### db.collectionName.find(query, projection)

    Retrieves documents from a collection matching a query.

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
