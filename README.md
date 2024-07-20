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

- find() Method: This method is used to search for documents in a MongoDB collection.
  Find all documents where name is "Alice".

- Query Parameter: The { key: "value" } part is a query that specifies the condition to match documents.

Let’s say you have a collection called books with the following documents:

- { "\_id": 1, "title": "The Great Gatsby", "author": "F. Scott Fitzgerald" }
- { "\_id": 2, "title": "To Kill a Mockingbird", "author": "Harper Lee" }
- { "\_id": 3, "title": "1984", "author": "George Orwell" }

If you want to find all documents where the author is "George Orwell", you would use:

- db.books.find({ author: "George Orwell" })

You would get:

- { "\_id": 3, "title": "1984", "author": "George Orwell" }

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

     Retrieves a single document that matches the query.
     Assume you have a collection named employees with the following documents:

- { "\_id": 1, "name": "Alice", "position": "Engineer" }
- { "\_id": 2, "name": "Bob", "position": "Manager" }
- { "\_id": 3, "name": "Charlie", "position": "Designer" }

  To find the document where name is "Bob", you would use:

- db.employees.findOne({ name: "Bob" })

Result:

- { "\_id": 2, "name": "Bob", "position": "Manager" }

### Using find() with Limit

    Retrieves documents that match the query. If you want to limit the result to one document, you use the limit() method.

- db.collectionName.find({ key: "value" }).limit(1)

  Using the same employees collection, to find the document where name is "Charlie":

- db.employees.find({ name: "Charlie" }).limit(1)

  Result:

- { "\_id": 3, "name": "Charlie", "position": "Designer" }

  findOne(): Retrieves a single document matching the criteria.
  find().limit(1): Retrieves documents matching the criteria, limited to one document.

### Find a Document by Using the $in Operator

    $in Operator: It is used to specify multiple possible values for a field. MongoDB will return documents where the field’s value matches any value in the array.

- db.collectionName.find({ fieldName: { $in: [value1, value2, ...] } })

  Let’s say you have a collection called products with the following documents:

- { "\_id": 1, "name": "Laptop", "category": "Electronics" }
- { "\_id": 2, "name": "Coffee Maker", "category": "Appliances" }
- { "\_id": 3, "name": "Smartphone", "category": "Electronics" }
- { "\_id": 4, "name": "Desk Chair", "category": "Furniture" }
- { "\_id": 5, "name": "Blender", "category": "Appliances" }

  To find all documents where the category is either "Electronics" or "Appliances", you would use:

- db.products.find({ category: { $in: ["Electronics", "Appliances"] } })

  The query would return:

- { "\_id": 1, "name": "Laptop", "category": "Electronics" }
- { "\_id": 2, "name": "Coffee Maker", "category": "Appliances" }
- { "\_id": 3, "name": "Smartphone", "category": "Electronics" }
- { "\_id": 5, "name": "Blender", "category": "Appliances" }

### Find a Document by Using the $eq Operator

    The $eq operator is optional in many cases as equality is the default comparison. You can achieve the same result with:

- db.products.find({ price: 800 })

  The $eq operator in MongoDB is used to specify equality in queries. It’s often used in the find() method to retrieve documents where a field equals a specified value.

- db.collectionName.find({ field: { $eq: value } })

  Assume you have a collection named products with the following documents:

- { "\_id": 1, "productName": "Laptop", "price": 1200 }
- { "\_id": 2, "productName": "Smartphone", "price": 800 }
- { "\_id": 3, "productName": "Tablet", "price": 400 }

  To find the document where the price is exactly $800 using the $eq operator:

- db.products.find({ price: { $eq: 800 } })

  Result:

- { "\_id": 2, "productName": "Smartphone", "price": 800 }

## Finding Documents By Using Comparisons Operators

    Example Collection
    Assume you have a collection named products with the following documents:

- { "\_id": 1, "productName": "Laptop", "price": 1200, "quantity": 10 }
- { "\_id": 2, "productName": "Smartphone", "price": 800, "quantity": 15 }
- { "\_id": 3, "productName": "Tablet", "price": 400, "quantity": 20 }
- { "\_id": 4, "productName": "Monitor", "price": 300, "quantity": 5 }
- { "\_id": 5, "productName": "Mouse", "price": 25, "quantity": 50 }

### $gt (Greater Than)

    Finds documents where the field value is greater than the specified value.

- db.products.find({ price: { $gt: 500 } })

  Result:

- { "\_id": 1, "productName": "Laptop", "price": 1200, "quantity": 10 }
- { "\_id": 2, "productName": "Smartphone", "price": 800, "quantity": 15 }

### $lt (Less Than)

    Finds documents where the field value is less than the specified value.

- db.products.find({ price: { $lt: 500 } })

  Result:

- { "\_id": 3, "productName": "Tablet", "price": 400, "quantity": 20 }
- { "\_id": 4, "productName": "Monitor", "price": 300, "quantity": 5 }
- { "\_id": 5, "productName": "Mouse", "price": 25, "quantity": 50 }

### $gte (Greater Than or Equal To)

    Finds documents where the field value is greater than or equal to the specified value.

- db.products.find({ price: { $gte: 400 } })

  Result:

* { "\_id": 1, "productName": "Laptop", "price": 1200, "quantity": 10 }
* { "\_id": 2, "productName": "Smartphone", "price": 800, "quantity": 15 }
* { "\_id": 3, "productName": "Tablet", "price": 400, "quantity": 20 }

### $lte (Less Than or Equal To)

    Finds documents where the field value is less than or equal to the specified value.

- db.products.find({ price: { $lte: 400 } })

  Result:

* { "\_id": 3, "productName": "Tablet", "price": 400, "quantity": 20 }
* { "\_id": 4, "productName": "Monitor", "price": 300, "quantity": 5 }
* { "\_id": 5, "productName": "Mouse", "price": 25, "quantity": 50 }

### $ne (Not Equal To)

    Finds documents where the field value is not equal to the specified value.

- db.products.find({ price: { $ne: 800 } })

  Result:

* { "\_id": 1, "productName": "Laptop", "price": 1200, "quantity": 10 }
* { "\_id": 3, "productName": "Tablet", "price": 400, "quantity": 20 }
* { "\_id": 4, "productName": "Monitor", "price": 300, "quantity": 5 }
* { "\_id": 5, "productName": "Mouse", "price": 25, "quantity": 50 }

## Querying on Array Elements in MongoDB

### $elemMatch

    It is crucial when you want to ensure that multiple criteria apply to the same array element.  Matches documents that contain an array with at least one element that matches all specified criteria.

    Suppose we have a collection orders with the following documents:

- [
  - { "\_id": 1, "items": [{ "name": "Laptop", "quantity": 2 }, { "name": "Mouse", "quantity": 1 }] },
  - { "\_id": 2, "items": [{ "name": "Phone", "quantity": 1 }, { "name": "Charger", "quantity": 2 }] },
  - { "\_id": 3, "items": [{ "name": "Laptop", "quantity": 1 }, { "name": "Phone", "quantity": 3 }] }
- ]

  Find documents where there is an item with name "Laptop" and quantity greater than 1:

* db.orders.find({
  - items: { $elemMatch: { name: "Laptop", quantity: { $gt: 1 } } }
* });

  Result:

* [
  - { "\_id": 1, "items": [{ "name": "Laptop", "quantity": 2 }, { "name": "Mouse", "quantity": 1 }] }
* ]

  #### Without Using $elemMatch

  Find documents where any item has name "Laptop" and any item has quantity greater than 1:

* db.orders.find({
* "items.name": "Laptop",
* "items.quantity": { $gt: 1 }
* });

  Result:

* [

- { "\_id": 1, "items": [{ "name": "Laptop", "quantity": 2 }, { "name": "Mouse", "quantity": 1 }] },
- { "\_id": 3, "items": [{ "name": "Laptop", "quantity": 1 }, { "name": "Phone", "quantity": 3 }] }

* ]

#### Using $elemMatch:

    The $elemMatch operator ensures that both conditions (name: "Laptop" and quantity: { $gt: 1 }) are satisfied by the same element in the array.
    This is useful when you need to apply multiple conditions to the same subdocument.

#### Without $elemMatch:

    The query checks each condition independently across all elements in the array.
    It may return documents where one element matches name: "Laptop" and another separate element matches quantity: { $gt: 1 }.

## Finding Documents By Using Logical Operators

    Suppose we have a collection products with the following documents:

- [
  - { "\_id": 1, "name": "Laptop", "price": 1200, "category": "electronics" },
  - { "\_id": 2, "name": "Phone", "price": 800, "category": "electronics" },
  - { "\_id": 3, "name": "Shoes", "price": 100, "category": "clothing" },
  - { "\_id": 4, "name": "Watch", "price": 200, "category": "accessories" }
- ]

### $and

    Find documents where both conditions are true.

    Find electronics with a price greater than $500.

- db.products.find({
  - $and: [
  - { category: "electronics" },
  - { price: { $gt: 500 } }
  - ]
- });

Result:

- [
  - { "\_id": 1, "name": "Laptop", "price": 1200, "category": "electronics" },
  - { "\_id": 2, "name": "Phone", "price": 800, "category": "electronics" }
- ]

### $or

    Find documents where at least one condition is true.
    Example: Find items that are either electronics or cost less than $150.

- db.products.find({
  - $or: [
    - { category: "electronics" },
    - { price: { $lt: 150 } }
  - ]
- });

  Result:

* [
  - { "\_id": 1, "name": "Laptop", "price": 1200, "category": "electronics" },
  - { "\_id": 2, "name": "Phone", "price": 800, "category": "electronics" },
  - { "\_id": 3, "name": "Shoes", "price": 100, "category": "clothing" }
* ]

### $not

    Find documents where the condition is not true.
    Inverts a condition, selecting documents where the condition is false.

### $nor

    Find documents where none of the conditions are true.
    Combines multiple conditions that must all be false.

### $and with Nested $or

    Find documents where:

- The price is less than 1000
- And the item is either a "computer" or "mobile"

  Nesting $or within $and lets you create complex queries where you want all conditions of $and to be true, but any condition within $or to be true.

- db.products.find({
  - $and: [
  - { price: { $lt: 1000 } },
  - { $or: [
    - { tags: "computer" },
    - { tags: "mobile" }
  - ]
  - }
  - ]
- });

## Replacing a Document in MongoDB

    This operation completely replaces an existing document with a new one.
    Here's an explanation of its parameters:

- db.collection.replaceOne(
  - <filter>,
  - <replacement>,
  - <options>
- )

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
