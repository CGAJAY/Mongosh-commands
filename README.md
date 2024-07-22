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
  - filter,
  - replacement,
  - options
- )

  Parameters
  filter

  - Description: Specifies the criteria to find the document to replace.
  - Type: Object
  - Example: { \_id: 1 } to match a document by its unique identifier.

    replacement

    - Description: The new document that will replace the existing one.
    - Type: Object.
    - Note: The \_id field must be included if you want to keep it the same.
    - Example: { name: "John", age: 30 }

    options

    - Description: Optional settings to modify the behavior of the operation.
    - Type: Object
    - Common Options:
    - upsert: If true, creates a new document if no matching document is found.
    - Default is false.
      Example: { upsert: true }

## Updating MongoDB Documents

### updateOne()

    updates a single document that matches the filter criteria.

    Parameters

- Filter: Specifies the criteria to match the document.
- Update: Defines the update operations to apply.
- Options: Optional settings for the update operation.
- Example Collection
- Suppose we have a collection users:

  [
  { "_id": 1, "name": "Alice", "age": 28, "city": "New York" },
  { "_id": 2, "name": "Bob", "age": 34, "city": "Chicago" }
  ]

  Example of updateOne()
  Let's update Bob's age:

* db.users.updateOne(
* { name: "Bob" }, // Filter
* { $set: { age: 35 } }, // Update
* { upsert: false } // Options
* );

Resulting Collection:

- [
- { "\_id": 1, "name": "Alice", "age": 28, "city": "New York" },
- { "\_id": 2, "name": "Bob", "age": 35, "city": "Chicago" }
- ]

## Update Operators

### $set: Sets the value of a field.

{ $set: { age: 35 } }

### $inc: Increments the value of a field.

    { $inc: { age: 1 } }

### $unset: Removes a field from a document.

    { $unset: { city: "" } }

### $rename: Renames a field.

    { $rename: { city: "location" } }

### $addToSet: Adds an element to an array if it doesn't exist.

    { $addToSet: { hobbies: "reading" } }

### $push: Adds an element to the end of an array.

    { $push: { hobbies: "reading" } }

### Options

### upsert: Creates a new document if no document matches the filter.

{ upsert: true }

### arrayFilters: Specifies filters for array elements when updating arrays.

    {
    arrayFilters: [{ "elem.age": { $gt: 30 } }]
    }

### Explanation

    Filter: Determines which document to update.
    Update: Specifies changes using update operators.
    Options: Adjusts the behavior of the update operation.
    updateOne() is powerful for making precise updates to your MongoDB documents.

## Updating MongoDB Documents by Using findAndModify()

    findAndModify() is used to update documents and return the modified document.

    Suppose we have a collection products:

- [
  - { "\_id": 1, "name": "Laptop", "price": 1200 },
  - { "\_id": 2, "name": "Phone", "price": 800 }
- ]

  Example: Update and Return Modified Document
  Let's increase the price of the laptop by 100 and return the updated document:

  - db.products.findAndModify({
    - query: { \_id: 1 },
    - update: { $inc: { price: 100 } },
    - new: true
  - });

  Result:
  The document returned will be:

  - { "\_id": 1, "name": "Laptop", "price": 1300 }

  Explanation

  - query: Specifies the document to update (\_id: 1).
  - update: Defines the update operation ($inc increases the price by 100).
  - new: true: Returns the updated document. By default, it returns the original document

#### Return Value:

    findAndModify() returns the modified document (if new: true is set).
    updateOne() returns a write result object containing details about the operation, but not the document itself.

#### Use Case:

    findAndModify() is useful when you need to update a document and immediately use the modified version.
    updateOne() is used when you only need to apply changes without needing the updated document immediately.

### db.collection.updateMany(filter, update, options)

    is used to update multiple documents that match a given filter.

    Suppose we have a collection products with the following documents:

- [
  - { "\_id": 1, "name": "Laptop", "price": 1200, "category": "electronics" },
  - { "\_id": 2, "name": "Phone", "price": 800, "category": "electronics" },
  - { "\_id": 3, "name": "Shoes", "price": 100, "category": "clothing" },
  - { "\_id": 4, "name": "Tablet", "price": 600, "category": "electronics" }
- ]

  Using updateMany()
  Increase Price of All Electronics
  Suppose we want to increase the price of all electronics by 10%.

  - db.products.updateMany(
    - { category: "electronics" }, // Filter: Match electronics
    - { $mul: { price: 1.1 } } // Update: Multiply price by 1.1
  - );

            Resulting Collection:

        - [
          - { "\_id": 1, "name": "Laptop", "price": 1320, "category": "electronics" },
          - { "\_id": 2, "name": "Phone", "price": 880, "category": "electronics" },
          - { "\_id": 3, "name": "Shoes", "price": 100, "category": "clothing" },
          - { "\_id": 4, "name": "Tablet", "price": 660, "category": "electronics" }
        - ]

        #### Filter: { category: "electronics" }

        Matches all documents where the category is "electronics".

        #### Update: { $mul: { price: 1.1 } }

        Multiplies the price field by 1.1, effectively increasing the price by 10%.

        #### options (Optional)

        upsert: If true, creates a new document if no documents match the filter.
        Default: false
        Example: { upsert: true }

    #### Key Points

    Multiple Updates: updateMany() affects all documents matching the filter.
    Atomic Operations: Uses operators like $set, $inc, $mul, etc., to modify fields.
    No Effect on Non-matching Documents: Only updates documents that meet the filter criteria.
    This method is powerful for bulk updates in a collection.

## Deleting Documents in MongoDB

### deleteOne(filter)

    Deletes a single document that matches the filter criteria.

- filter: Criteria to match the document you want to delete.

  Example: { name: "Alice" }

- options (Optional): Specifies language-specific rules for string comparison.
- Example: { locale: "en", strength: 2 }
  - db.collection.deleteOne(
  - { name: "Alice" }
  - );
    This deletes the first document where the name is "Alice".

### deleteMany(filter)

Deletes all documents that match the filter criteria.
filter: Criteria to match the documents you want to delete.

    Example: { status: "inactive" }

    options (Optional):
    Specifies language-specific rules for string comparison.

- db.collection.deleteMany(
- { status: "inactive" }
- );
  This deletes all documents with a status of "inactive".

### findOneAndDelete(filter)

    Finds a single document and deletes it, returning the deleted document.

    filter:
    Criteria to match the document you want to delete.

- Example: { age: { $gt: 30 } }

  options (Optional):
  Specifies fields to return in the document.

  - Example: { name: 1, \_id: 0 }

    sort:
    Determines which document to delete if multiple documents match the filter.

    - Example: { age: -1 } (deletes the oldest first)

      collation:
      Specifies language-specific rules for string comparison.

      Example

      - db.collection.findOneAndDelete(
      - { age: { $gt: 30 } },
      - { sort: { age: -1 } }
      - );
        This deletes and returns the oldest person over 30.

    Summary
    deleteOne(): Deletes the first matching document.
    deleteMany(): Deletes all matching documents.
    findOneAndDelete(): Finds, deletes, and returns a single document based on the criteria.

## Sorting and Limiting Query Results in MongoDB

### sort()

The sort() method specifies the order in which documents are returned.

- db.collection.find().sort({ field: direction })
- field: The field by which to sort the documents.
- direction: The sort direction, where 1 indicates ascending order and -1 indicates descending order.

  Example:
  Suppose you have a products collection with the following documents:

  - [
    - { "\_id": 1, "name": "Laptop", "price": 1200 },
    - { "\_id": 2, "name": "Phone", "price": 800 },
    - { "\_id": 3, "name": "Tablet", "price": 600 }
  - ]

    Sort by price in ascending order:

    - db.products.find().sort({ price: 1 });

    Sort by price in descending order:

    - db.products.find().sort({ price: -1 });

### limit()

Limiting the number of results returned can be done using the limit() method. The limit() method specifies the maximum number of documents to return.

- db.collection.find().limit(number)
- number: The maximum number of documents to return.

Example:
Limit to 2 documents:

- db.products.find().limit(2);

### Combining Sorting and Limiting

You can combine both sort() and limit() methods to sort documents and then limit the number of results.

Example:
Sort by price in descending order and limit to 2 documents:

- db.products.find().sort({ price: -1 }).limit(2);

### Sorting and Limiting with Pagination

For pagination, you often combine skip() with limit(). The skip() method specifies the number of documents to skip before returning results.

- db.collection.find().skip(number).limit(number)
- number: The number of documents to skip or limit.

  Example:
  Skip the first 2 documents and limit the results to 2 documents:

  - db.products.find().skip(2).limit(2);

    Summary
    sort(): Orders the documents based on specified fields and directions.
    limit(): Restricts the number of documents returned.
    skip(): Skips a specified number of documents, often used with limit() for pagination.

## Returning Specific Data from a Query in MongoDB

    To specify fields to include or exclude in the result set, add a projection document as the second parameter in the call to db.collection.find().

#### To include a field, set its value to 1 in the projection document.

- db.collection.find( <query>, { <field> : 1 })

  Example:

  Return all restaurant inspections - business name, result, and \_id fields only

  - db.inspections.find(
    - { sector: "Restaurant - 818" },
    - { business_name: 1, result: 1 }
  - )

#### To exclude a field, set its value to 0 in the projection document.

- db.collection.find(query, { <field> : 0, <field>: 0 })

  Example:

  Return all inspections with result of "Pass" or "Warning" - exclude date and zip code

  - db.inspections.find(
    - { result: { $in: ["Pass", "Warning"] } },
    - { date: 0, "address.zip": 0 }
  - )

  #### While the \_id field is included by default, it can be suppressed by setting its value to 0 in any projection.

  Return all restaurant inspections - business name and result fields only

  - db.inspections.find(
    - { sector: "Restaurant - 818" },
    - { business_name: 1, result: 1, \_id: 0 }
  - )

## Counting Documents in a MongoDB Collection

### countDocuments()

    is used to count the number of documents in a collection that match a specified filter.countDocuments() takes two parameters: a query document and an options document.

- db.collection.countDocuments(query, options)

query (Optional)

- Description: Specifies the criteria to filter documents.
- Example: { status: "active" } counts documents with the status field set to "active".

options (Optional)

- limit: Restricts the count to a specified number of documents.
- Example: { limit: 10 } counts only up to 10 documents.

skip: Skips a specified number of documents before counting.

- Example: { skip: 5 } skips the first 5 documents.

hint: Forces MongoDB to use a specific index for the count.

- Example: { hint: "_id_" } uses the \_id index.

#### Count All Documents

- db.users.countDocuments();

#### Count Documents with a Filter

- db.users.countDocuments({ age: { $gte: 18 } });

#### Count with Options

- db.users.countDocuments(
  - { age: { $gte: 18 } },
  - { limit: 5, skip: 2 }
- );

#### Explanation

- No Filter: Counts all documents in the collection.
- Filter: Counts documents matching the specified criteria.
- Options: Further refine the count operation using limit, skip, and hint.
- Key Points
- Efficient Counting: countDocuments() is optimized for counting documents with filters.

* Options: Useful for pagination or performance tuning with indexes.

## Introduction to MongoDB Aggregation

Aggregation: Collection and summary of data

Stage: One of the built-in methods that can be completed on the data, but does not permanently alter it

Aggregation pipeline: A series of stages completed on the data in order or sequence of stages, where each stage transforms the documents as they pass through.

- db.collection.aggregate([
-     {
-         $stage1: {
-             { expression1 },
-             { expression2 }...
-         },
-         $stage2: {
-             { expression1 }...
-         }
-     }
- ])

  Using $match and $group Stages in a MongoDB Aggregation Pipeline

### $match

    The $match stage filters for documents that match specified conditions.

- { $match: { product: "laptop" } }
- Selects sales documents where the product is "laptop".

### $group

     is used to group documents by a specified field and perform aggregate operations on each group. This stage is similar to the SQL GROUP BY clause.

- {
- $group: {
-     _id: <expression>,
-     <field1>: { <accumulator1>: <expression> },
-     <field2>: { <accumulator2>: <expression> },
-     ...
- }
- }

#### Key Components

- \_id: Specifies the field or expression to group documents by. Each unique value of \_id creates a new group.

- field: Defines fields to include in the output. Use accumulator operators to calculate values for these fields.

#### Common Accumulator Operators

- $sum: Calculates the sum of numeric values.
- $avg: Calculates the average of numeric values.
- $max: Finds the maximum value.
- $min: Finds the minimum value.
- $first: Returns the first value in the group.
- $last: Returns the last value in the group.

#### Example 1: Sum of Sales by Region

- db.sales.aggregate([
- {
-     $group: {
-       _id: "$region",
-       totalSales: { $sum: "$amount" }
-     }
- }
- ])

#### Explanation:

- \_id: "$region": Groups documents by the region field.
- totalSales: { $sum: "$amount" }: Calculates the total sales amount for each region.

#### Example 2: Average Age by Department

- db.employees.aggregate([
- {
-     $group: {
-       _id: "$department",
-       averageAge: { $avg: "$age" }
-     }
- }
- ])

#### Explanation:

- \_id: "$department": Groups documents by the department field.
- averageAge: { $avg: "$age" }: Calculates the average age of employees in each department.

#### Example 3: Maximum and Minimum Scores by Subject

- db.exams.aggregate([
- {
-     $group: {
-       _id: "$subject",
-       highestScore: { $max: "$score" },
-       lowestScore: { $min: "$score" }
-     }
- }
- ])

#### Explanation:

- \_id: "$subject": Groups documents by the subject field.
- highestScore: { $max: "$score" }: Finds the highest score for each subject.
- lowestScore: { $min: "$score" }: Finds the lowest score for each subject.

#### Summary

    Grouping: The $group stage organizes documents into groups based on the _id field.
    Aggregation: Use accumulator operators to calculate aggregated values for each group.
    Flexibility: Allows complex data summarization and analysis.

### Combining $match and $group

#### Filter Data First ($match)

Start by using $match to filter the documents based on some criteria. This step reduces the dataset to relevant documents.

#### Aggregate Data ($group)

After filtering, use $group to perform aggregation operations like summing values, counting documents, or calculating averages.

#### Example Scenario

Imagine you have a sales collection with the following documents:

- [
- { "product": "laptop", "region": "North", "amount": 1200 },
- { "product": "laptop", "region": "South", "amount": 1500 },
- { "product": "phone", "region": "North", "amount": 800 },
- { "product": "laptop", "region": "North", "amount": 1100 },
- { "product": "phone", "region": "South", "amount": 700 }
- ]

#### Goal

Find the total sales amount for "laptop" in each region.

Aggregation Pipeline

- db.sales.aggregate([
- { $match: { product: "laptop" } }, // Step 1: Filter documents where product is "laptop"
- { $group: { _id: "$region", totalSales: { $sum: "$amount" } } } // Step 2: Group by region and sum amounts
- ])

#### Explanation

    $match: Filters the documents to include only those where the product is "laptop".

- { $match: { product: "laptop" } }

#### Resulting documents:

- [
- { "product": "laptop", "region": "North", "amount": 1200 },
- { "product": "laptop", "region": "South", "amount": 1500 },
- { "product": "laptop", "region": "North", "amount": 1100 }
- ]

  $group: Groups the filtered documents by region and calculates the total amount for each region.

- { $group: { _id: "$region", totalSales: { $sum: "$amount" } } }

#### Result:

- [
- { "\_id": "North", "totalSales": 2300 },
- { "\_id": "South", "totalSales": 1500 }
- ]

#### Summary

    $match filters the data to include only relevant documents.

    $group performs aggregation on the filtered data.

### Using $sort and $limit Stages in a MongoDB Aggregation Pipeline

In a MongoDB aggregation pipeline, the $sort and $limit stages are used to control the ordering and quantity of documents in the results

### $sort

The $sort stage sorts all input documents and returns them to the pipeline in sorted order. We use 1 to represent ascending order, and -1 to represent descending order.

- Syntax: { $sort: { field1: 1, field2: -1 } }
- 1: Ascending order.
- -1: Descending order

### $limit

The $limit stage returns only a specified number of records.

- Syntax: { $limit: n }
- n: The maximum number of documents to return.

### Combining $sort and $limit

You can use $sort to order your documents and $limit to restrict the number of documents returned. This is useful for tasks like finding the top N results based on certain criteria.

Suppose you have a sales collection with the following documents:

- [
- { "product": "laptop", "amount": 1200, "date": ISODate("2024-07-01T00:00:00Z") },
- { "product": "phone", "amount": 700, "date": ISODate("2024-07-02T00:00:00Z") },
- { "product": "tablet", "amount": 300, "date": ISODate("2024-07-03T00:00:00Z") },
- { "product": "laptop", "amount": 1500, "date": ISODate("2024-07-04T00:00:00Z") },
- { "product": "laptop", "amount": 900, "date": ISODate("2024-07-05T00:00:00Z") }
- ]

#### Goal

Find the top 2 sales amounts for laptops, sorted by the highest amount.

- db.sales.aggregate([
- { $match: { product: "laptop" } }, // Filter to include only laptops
- { $sort: { amount: -1 } }, // Sort by amount in descending order
- { $limit: 2 } // Limit to the top 2 results
- ])

#### Explanation

$match: Filters the documents to include only those where product is "laptop".

- { $match: { product: "laptop" } }

#### Resulting documents:

- [
- { "product": "laptop", "amount": 1200, "date": ISODate("2024-07-01T00:00:00Z") },
- { "product": "laptop", "amount": 1500, "date": ISODate("2024-07-04T00:00:00Z") },
- { "product": "laptop", "amount": 900, "date": ISODate("2024-07-05T00:00:00Z") }
- ]

  $sort: Sorts the filtered documents by amount in descending order.

- { $sort: { amount: -1 } }

Sorted documents:

- [
- { "product": "laptop", "amount": 1500, "date": ISODate("2024-07-04T00:00:00Z") },
- { "product": "laptop", "amount": 1200, "date": ISODate("2024-07-01T00:00:00Z") },
- { "product": "laptop", "amount": 900, "date": ISODate("2024-07-05T00:00:00Z") }
- ]

  $limit: Limits the result to the top 2 documents.

- { $limit: 2 }

#### Final result:

- [
- { "product": "laptop", "amount": 1500, "date": ISODate("2024-07-04T00:00:00Z") },
- { "product": "laptop", "amount": 1200, "date": ISODate("2024-07-01T00:00:00Z") }
- ]

## Using $project, $count, and $set Stages in a MongoDB Aggregation Pipeline

- [
- { "name": "Alice", "score": 85, "class": "Math" },
- { "name": "Bob", "score": 90, "class": "Science" },
- { "name": "Charlie", "score": 75, "class": "Math" },
- { "name": "David", "score": 92, "class": "Science" },
- { "name": "Eve", "score": 48, "class": "Math" }
- ]

### $project

The $project stage specifies the fields of the output documents. 1 means that the field should be included, and 0 means that the field should be supressed. The field can also be assigned a new value.
Include only the name and create a new field passed that indicates if a student scored 50 or more.

- db.students.aggregate([
- {
-     $project: {
-       name: 1,
-       passed: { $gte: ["$score", 50] }
-     }
- }
- ])

#### Explanation

name: 1: Includes the name field.
passed: A new field set to true if score is 50 or more, false otherwise.

- [
- { "name": "Alice", "passed": true },
- { "name": "Bob", "passed": true },
- { "name": "Charlie", "passed": true },
- { "name": "David", "passed": true },
- { "name": "Eve", "passed": false }
- ]

### $count

The $count stage creates a new document, with the number of documents at that stage in the aggregation pipeline assigned to the specified field name.

#### Goal

Count how many students passed.

- db.students.aggregate([
- { $match: { score: { $gte: 50 } } },
- { $count: "passedStudents" }
- ])

#### Explanation

$match: Filters students with a score of 50 or more.
$count: Counts these filtered documents.

#### output

- [
- { "passedStudents": 4 }
- ]

### $set

The $set stage creates new fields or changes the value of existing fields, and then outputs the documents with the new fields.

#### Goal

Add a field honors to indicate if a student scored 90 or more.

- db.students.aggregate([
- {
- $set: {
-       honors: { $gte: ["$score", 90] }
- }
- }
- ])

#### Explanation

honors: A new field set to true if score is 90 or more.

- [
- { "name": "Alice", "score": 85, "class": "Math", "honors": false },
- { "name": "Bob", "score": 90, "class": "Science", "honors": true },
- { "name": "Charlie", "score": 75, "class": "Math", "honors": false },
- { "name": "David", "score": 92, "class": "Science", "honors": true },
- { "name": "Eve", "score": 48, "class": "Math", "honors": false }
- ]

#### Summary

- $project: Selects fields and creates new ones.
- $count: Provides a total count of documents after filtering.
- $set: Adds or modifies fields within documents.

### $out Stage

writes the results of an aggregation pipeline to a specified collection.
Use it to save the output of a pipeline to a new or existing collection.
Overwrites the entire collection if it exists.
If the collection does not exist, it creates a new one.

#### Goal

Filter students who passed and save the results to a new collection called passed_students.

Initial students Collection

- [
- { "name": "Alice", "score": 85, "class": "Math" },
- { "name": "Bob", "score": 90, "class": "Science" },
- { "name": "Charlie", "score": 75, "class": "Math" },
- { "name": "David", "score": 92, "class": "Science" },
- { "name": "Eve", "score": 48, "class": "Math" }
- ]

Aggregation Pipeline

- db.students.aggregate([
- { $match: { score: { $gte: 50 } } }, // Filter students who passed
- { $out: "passed_students" } // Save the results to the passed_students collection
- ])

#### Explanation

$match: Filters the documents to include only students with a score of 50 or more.
$out: Writes the filtered documents to the passed_students collection.

#### Output

The passed_students collection will contain:

- [
- { "name": "Alice", "score": 85, "class": "Math" },
- { "name": "Bob", "score": 90, "class": "Science" },
- { "name": "Charlie", "score": 75, "class": "Math" },
- { "name": "David", "score": 92, "class": "Science" }
- ]

#### Summary

$out is used to store the result of an aggregation pipeline in a new or existing collection.
It helps persist the transformed data for future use or analysis.

### db.collection.find( <query>, <projection> )

### db.collection.deleteOne(filter)

     Deletes a single document.

### db.collection.deleteMany(filter)

     Deletes multiple documents.

### db.collection.replaceOne(filter, replacement)

     Replaces a document.

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
