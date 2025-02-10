
# MongoDB Basics: A Story of the School Database

Welcome to our MongoDB adventure! In this guide, we will learn basic MongoDB commands such as show dbs, use, createCollection, insert, update, remove, and many more. We will create a sample database, add a collection, insert various types of data, update documents, and query our data using different techniques. Let’s begin our journey!

## 1. Checking Available Databases
Before we start, let’s see which databases are available on our MongoDB server:

```javascript
> show dbs
```
This command lists all the databases that already exist on your MongoDB instance.

## 2. Creating and Using a New Database
Our story begins with a new database named schoolDB. Use the following command to create and switch to it:

```javascript
> use schoolDB
```

MongoDB creates the database only when you insert data into it.

## 3. Creating a Collection
Next, let’s create a collection called students. This collection will store our student documents.

```javascript
> db.createCollection("students")
```
Although MongoDB creates collections on the fly when you first insert a document, explicitly creating one can be useful for setting options.

## 4. Inserting Data with Different Data Types
Let’s populate our collection with some sample data. We’ll include various data types such as strings, numbers, booleans, arrays, objects, dates, and even a null value.

### 4.1. Inserting a Single Document
```javascript
> db.students.insertOne({
    name: "Alice Johnson",
    age: 14,
    enrolled: true,
    subjects: ["Mathematics", "Science", "History"],
    contact: {
        email: "alice@example.com",
        phone: null
    },
    enrollmentDate: new Date("2023-09-01")
})
```
### 4.2. Inserting Multiple Documents
```javascript
> db.students.insertMany([
    {
        name: "Bob Smith",
        age: 15,
        enrolled: false,
        subjects: ["English", "Art"],
        contact: { email: "bob@example.com", phone: "123-456-7890" },
        enrollmentDate: new Date("2022-09-01")
    },
    {
        name: "Charlie Brown",
        age: 14,
        enrolled: true,
        subjects: ["Mathematics", "Physical Education"],
        contact: { email: "charlie@example.com", phone: "098-765-4321" },
        enrollmentDate: new Date("2023-01-15")
    }
])
```
## 5. Using a Loop to Insert Sample Data
Sometimes you may want to insert several documents quickly. Here’s how you can use a JavaScript for loop within mongosh to add sample data.

```javascript
for (let i = 1; i <= 5; i++) {
    db.students.insertOne({
        name: "Student " + i,
        age: Math.floor(Math.random() * (18 - 13 + 1)) + 13,  // random age between 13 and 18
        enrolled: i % 2 === 0,  // alternate enrolled status
        subjects: ["Subject " + i, "Extra " + i],
        contact: { email: "student" + i + "@school.com", phone: null },
        enrollmentDate: new Date()
    })
}
```
This loop inserts 5 student documents with dynamically generated values.

## 6. Querying the Data
Now that we have data in our collection, let’s explore how to find and query documents.

### 6.1. Finding All Documents
```javascript
> db.students.find()
```
This command returns a cursor to all documents in the students collection.

### 6.2. Pretty-Print the Results
```javascript
> db.students.find().pretty()
```
The .pretty() method formats the output to be more readable.

### 6.3. Finding Documents with a Specific Condition
Let’s find all students who are enrolled:

```javascript
> db.students.find({ enrolled: true })
```
### 6.4. Using Comparison Operators
To find students older than 14:

```javascript
> db.students.find({ age: { $gt: 14 } }).pretty()
```
The $gt operator stands for "greater than". Similarly, $lt is "less than", $gte is "greater than or equal", and $lte is "less than or equal".

## 7. Updating Documents
Suppose we want to update a student’s contact information or add a new subject.

### 7.1. Updating a Single Document
Let’s update Alice Johnson’s phone number:

```javascript
> db.students.updateOne(
    { name: "Alice Johnson" },
    { $set: { "contact.phone": "555-123-4567" } }
)
```
### 7.2. Updating Multiple Documents
Add a new subject to all students who are not enrolled:

```javascript
> db.students.updateMany(
    { enrolled: false },
    { $push: { subjects: "Remedial Classes" } }
)
```
The $push operator appends a new value to an array field.

## 8. Removing Documents
Maybe we want to remove a student record that was added by mistake.

### 8.1. Removing a Single Document
```javascript
> db.students.deleteOne({ name: "Bob Smith" })
```
### 8.2. Removing Multiple Documents
To remove all students who are not enrolled:

```javascript
> db.students.deleteMany({ enrolled: false })
```

Be cautious with the deleteMany command as it will remove all matching documents.

## 9. Conclusion
In this story, we have:

- Checked available databases with show dbs.
- Created and switched to a new database using use schoolDB.
- Created a collection called students.
- Inserted documents with a variety of data types using insertOne, insertMany, and a for loop.
- Queried the data using find with different filters and operators.
- Updated documents using updateOne and updateMany.
- Removed documents using deleteOne and deleteMany.
- These commands form the backbone of MongoDB operations. As you explore further, you'll find that these basic commands can be combined and extended to create powerful data manipulation scripts.

Happy coding with MongoDB!

