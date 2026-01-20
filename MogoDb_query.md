📘 MongoDB & Database Operations Wiki

Welcome to the Web Development – MongoDB Wiki 🚀
This document covers MongoDB basics, CRUD operations, query operators, and aggregation with clear examples.

🛠 MongoDB Shell Basics
Ctrl + L


➡️ Clears the MongoDB shell screen

use db-name


➡️ Switches to a database (creates it if it doesn’t exist)

show dbs


➡️ Shows all available databases

use school


➡️ Switch to school database

show collections


➡️ Lists all collections in the current database

📂 Collections
db.students


➡️ Creates a collection named students

db.createCollection("myCollection")


➡️ Explicitly creates a collection

db.books.drop()


➡️ Deletes the books collection

➕ Create (Insert) Operations
db.student.insertOne({ name: "john", age: 12 })

db.student.insertMany([
  { name: "sam", age: 12 },
  { name: "curn", age: 23 }
])

🔍 Read (Find) Operations
db.student.find()


➡️ Returns all documents (cursor)

db.student.findOne({ name: "sam" })


➡️ Returns a single document

db.student.find({ age: { $lt: 20 } })


➡️ Find students with age less than 20

Cursor Methods (only with find())
db.student.find().count()
db.student.find().limit(2)
db.student.find().toArray()
db.student.find().forEach(x => printjson(x))

✏️ Update Operations
db.student.updateOne(
  { name: "sam" },
  { $set: { age: 30 } }
)

db.student.updateMany(
  { age: 23 },
  { $set: { isEligible: false } }
)


➡️ $set also adds new fields if they don’t exist

❌ Delete Operations
db.student.deleteOne({ name: "sam" })

db.student.deleteMany({ isEligible: false })

db.student.deleteMany({})


➡️ Deletes all documents

📌 Nested Field Queries
db.student.updateOne(
  { name: "sam" },
  { $set: { idCard: { hasPanCard: false, hasAdharCard: true } } }
)

db.student.find({ "idCard.hasPanCard": false })

📚 CRUD Summary
Operation	Methods
Create	insertOne(), insertMany()
Read	find(), findOne()
Update	updateOne(), updateMany()
Delete	deleteOne(), deleteMany()
🔢 Comparison Operators
$eq   // equal
$ne   // not equal
$gt   // greater than
$gte  // greater than or equal
$lt   // less than
$lte  // less than or equal
$in   // inside array
$nin  // not inside array


Example:

db.student.find({ age: { $in: [23, 12] } })

🔀 Logical Operators
$or
$and
$nor


Example:

db.student.find({
  $or: [{ age: { $lt: 13 } }, { age: { $gt: 23 } }]
})

🧪 Query Operators
$exists
$type

db.student.find({ hasMacBook: { $exists: true } })
db.student.find({ hasMacBook: { $type: "bool" } })

📊 Querying Arrays
db.student.find({ hobbies: { $size: 2 } })

db.student.find({
  hobbies: { $all: ["cooking", "anime"] }
})

🔄 Aggregation Framework

Aggregation processes data through pipeline stages.

Syntax
db.collection.aggregate(pipeline, options)

Common Stages
Stage	Description
$match	Filters documents
$group	Groups & aggregates
$sort	Sorts documents
$project	Reshapes fields
$unwind	Flattens arrays
$limit	Limits results
$skip	Skips documents
Aggregation Examples
db.student.aggregate([
  { $match: { hobbies: "Tv shows" } }
])

db.student.aggregate([
  { $group: { _id: "$age" } }
])

db.student.aggregate([
  {
    $group: {
      _id: "$age",
      names: { $push: "$name" }
    }
  }
])

db.student.aggregate([
  {
    $group: {
      _id: null,
      avgAge: { $avg: "$age" }
    }
  }
])

db.student.aggregate([
  { $unwind: "$hobbies" },
  {
    $group: {
      _id: "$age",
      hobbies: { $addToSet: "$hobbies" }
    }
  }
])

🔐 Atomicity in MongoDB

"Either everything happens or nothing happens."

MongoDB guarantees atomicity at the document level

Multi-document atomicity requires transactions

✅ Notes

$ indicates MongoDB reserved operators

_id is included by default (disable with _id: 0)

$addToSet avoids duplicates

$push allows duplicates
