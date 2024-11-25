2024-11-19 22:29

Status: #baby 

Tags: [[Web Programming]]

---
# Mongo DB

## 0.0 What is Mongo DB?
---
MongoDB is a document database. It stores data in a type of JSON format called BSON, the records on mongo DB are all documents and the field could include include numbers, strings, booleans, arrays, or even nested documents.

Here we are going to see an example of the mongo DB document.
```json
{
	title: "Post Title 1",
	body: "Body of post.",
	category: "News",
	likes: 1,
	tags: ["news", "events"],
	date: Date()
}
```

## 1.0 Bases and Creating the DB
---
With the MongoDB Query [[Programming Knowledge#What is an API|API]]  are the main operation that you can make are the aggregation pipelines one and the CRUD (**C** - create, **R** - read, **U** - update, **D** - delete).

Let's see the main commands:

- For connect you db you need to open the terminal and type `mongosh` (if you have it install ofc).
- For see all the databases that we have in our mongo server type:
  ```bash
show dbs
	```
- For use it one you should type the command, that can also create a db.
	```bash
use <name of the db u want to use>
	```
- For create the first [[#1.1 Collection|collection]].
```bash
db.createCollectio("nameOfCollection")

or 

db.nameOfDB.insertOne("nameOfCollection")
```

### 1.1 Collection
MongoDB stores documents in collections. Collections are analogous to tables in relational databases
![[crud-annotated-collection.bakedsvg.svg]]

>[!warning] N.B
>Every time you are going to create a collection or a db is not created until you are not going to get is contenct.

## 2.0 Insert Documents
In mongo DB exist 2 methods for creating documents inside a collection.
### `insertOne()`

To insert a single document, use the `insertOne()` method.This method inserts a single object into the database.

Here an example of a creation of a document:
```bash
db.nameOfDB.insertOne({
	title: "First Document inside a  collection",
	body: "This is the body of the document",
	tags: ["News", "NodeJS"],
	links: 1 //like ids inside the relational dbs
	date: Date()
})
```

>[!note] N.B 
> If you try to insert documents into a collection that does not exist, MongoDB will create the collection automatically

### `insertMany()`

You can also insert many documents inside a db instead of one each time, with `insertMany`

Here an example of `insertMany()` function in use:
```jsx
db.nameOfDB.insertMany(
	{
		title: "First Document inside a  collection",
		body: "This is the body of the document",
		tags: ["News", "NodeJS"],
		links: 1 //like ids inside the relational dbs
		date: Date()
	},
	{
	    title: "Post Title 2",
	    body: "Body of post.",
	    category: "Technology",
	    likes: 2,
	    tags: ["news", "events"],
	    date: Date()
	}
)
```

## 3.0 Find something inside the collection
---
For finding reference or something inside the document in the collection we are going to use the command:
### `find()`

here is the way we are going to use the `find()` function inside our collection:
```bash
db.nameOfDB.find()
```
### `findOne()`

To select only one document, we can use the `findOne()` method. This method accepts a query object. If left empty,==it will return the first document it finds==.
```bash
db.nameOfDB.findOne()
```

We can also filtering the query by adding the value inside the round bracket with 
{_category_name_: _"something we want find"_},here an example:

```bash
db.nameOfDB.find({category: "New"})
```
### 3.1 Projection
Like the projection in the relational(proiezione nei database relazionali) database, here we can do the same with the `find()` function, inside of it we are going to insert the _name_of_date_ : `1` means include or `0` that's mean exclude from the projection.

Let's see an example:
```bash
db.nameOfDB.find({}, {_id: 0, title: 1, body: 1})
```
There is only one rule:
>[!warning] N.B
You cannot use both `0` and `1` in the same object. ==The only exception is the `_id`== field. You should either specify the fields you would like to include or the fields you would like to exclude.

## 4.0 Update 
To update an existing document we can use the `updateOne()` or `updateMany()` methods.The first parameter is a query object to define which document or documents should be updated. 
The second parameter is an object defining the updated data

So is gonna be like
```mongosh
db.nameOfDB.updateOne({title: "Title of the document"}, {$set: {name_date: value_to_change}})
```

with the operator `$set`we are going to edit the field, where the title  have  a title that we gave, for example the title: "Test 2" we edit the body from 'this is the body of this document' to "This is the second document inside the collection".
![[TerminalForMongoUpdate.png]]
### `updateMany()`
we are 
# Reference
---
 Tutorial from W3School here: [MongoDB](https://www.w3schools.com/mongodb/index.php)
 Official website of MongoDB: [Official Web Site](https://www.mongodb.com/docs/manual/core/views/) 

