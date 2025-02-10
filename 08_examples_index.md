# MongoDB Indexes: Examples and Usage
In this lesson, we will provide practical examples of how to create and use various types of indexes in MongoDB. Each example includes the command and a brief explanation of its purpose.

### Note:
Ensure you are connected to your MongoDB instance and using the appropriate database and collection before executing these commands.

## 1. Single Field Index
- Purpose:
Indexes a single field to speed up queries that filter or sort by that field.

- Example:

    ```javascript
    > db.students.createIndex({ name: 1 }) 
    ```
This command creates an ascending index on the name field in the students collection.

## 2. Compound Index
- Purpose:
Indexes multiple fields. Useful when queries filter or sort on multiple fields.

- Example:

    ```javascript
    > db.students.createIndex({ name: 1, age: -1 }) 
    ```
    This creates a compound index on the name (ascending) and age (descending) fields.

## 3. Multikey Index
- Purpose:
Automatically indexes array fields. Each element in the array is indexed.

- Example:

    Assume each student document has an array field called subjects.

    ```javascript
    > db.students.createIndex({ subjects: 1 }) 
    ```
    This creates an index on the subjects array. Each element in the array is indexed individually.

## 4. Text Index
- Purpose:
Enables full-text search on string content.

- Example:

    Assume you have a collection of articles with a content field.

    ```javascript
    > db.articles.createIndex({ content: "text" }) 
    ```
    This creates a text index on the content field, allowing for text search queries.

## 5. Hashed Index
- Purpose:
Indexes the hashed value of a field. Mainly used for sharding to distribute documents evenly.

- Example:

    Assume you want to index the username field for sharding purposes.

    ```javascript
    > db.users.createIndex({ username: "hashed" }) 
    ```
    This creates a hashed index on the username field.

## 6. Geospatial Indexes
MongoDB supports two main types of geospatial indexes:

### 6.1. 2d Index
- Purpose:
Indexes legacy coordinate pairs for simple 2D queries.

- Example:

    Assume each document has a location field with a coordinate pair.

    ```javascript
    > db.places.createIndex({ location: "2d" }) 
    ```
    This creates a 2d index on the location field.

### 6.2. 2dsphere Index
- Purpose:
Indexes GeoJSON objects for spherical geometry queries.

- Example:

    Assume your documents use GeoJSON format for location.

    ```javascript
    > db.places.createIndex({ location: "2dsphere" }) 
    ```
    This creates a 2dsphere index on the location field for accurate geospatial queries on a sphere.

## 7. TTL (Time To Live) Index
- Purpose:
Automatically removes documents after a specified period, useful for expiring data such as sessions or logs.

- Example:

    Assume documents have a createdAt field and you want to expire documents after 1 hour (3600 seconds).

    ```javascript
    > db.sessions.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 }) 
    ```
    This creates a TTL index on the createdAt field, automatically removing documents 1 hour after their creation.

## 8. Sparse Index
- Purpose:
Indexes only documents that contain the indexed field. Useful when the field is not present in every document.

- Example:

    Assume some documents in the students collection have an optional field nickname.

    ```javascript
    > db.students.createIndex({ nickname: 1 }, { sparse: true }) 
    ```
    This creates a sparse index on the nickname field, indexing only documents that include this field.

## 9. Partial Index
- Purpose:
Indexes only a subset of documents that meet a specified filter condition. Can reduce index size and improve performance.

- Example:

    Assume you want to index only active students with a status field equal to "active".

    ```javascript
    > db.students.createIndex({ status: 1 }, { partialFilterExpression: { status: { $eq: "active" } } }) 
    ```
    This creates a partial index on the status field for documents where status is "active".

## 10. Summary
Below is a consolidated list of the examples:

Single Field Index:
```javascript
db.students.createIndex({ name: 1 })
```
Compound Index:
```javascript
db.students.createIndex({ name: 1, age: -1 })
```
Multikey Index:
```javascript
db.students.createIndex({ subjects: 1 })
```
Text Index:
```javascript
db.articles.createIndex({ content: "text" })
```
Hashed Index:
```javascript
db.users.createIndex({ username: "hashed" })
```
Geospatial 2d Index:
```javascript
db.places.createIndex({ location: "2d" })
```
Geospatial 2dsphere Index:
```javascript
db.places.createIndex({ location: "2dsphere" })
```
TTL Index:
```javascript
db.sessions.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 })
```
Sparse Index:
```javascript
db.students.createIndex({ nickname: 1 }, { sparse: true })
```
Partial Index:
```javascript
db.students.createIndex({ status: 1 }, { partialFilterExpression: { status: { $eq: "active" } } })
```
By understanding and using these index examples, you can optimize your MongoDB queries, improve performance, and tailor your database to meet specific application needs.

Happy indexing!