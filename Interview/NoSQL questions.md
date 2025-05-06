
##### What is NoSQL and how does it differ from traditional SQL Databases

- NoSQL are a cataagory of database managment system design for large scale data storage and for massivly-paralell high performance processing across distributed systems
- NoSQL databases are schemaless and do not require ridiget table structures
- They are highly scailable in comparason to SQL databases allowing for better horozontal and virtical scaling

##### Explain the different types of NoSQL databases and provide examples for each.

- There are Four main type of NoSQL databases
	- Key-value stores
		- Redis
	- Document stores
		- MongoDB
	- Coloum family stores
		- Cassandra
	- Graff stores
		- Neo4j


##### What are the advantages and disadvantages of using NoSQL databases?

Advantages:
- Flexibillity
- Scalability
- Ability to handle unstructured and flexable data

Disadvantages:
- Lack of standardization across the system

##### Describe the CAP theorem and its significance in NoSQL databases.

The CAP theorem infers that a dustrabuted system can only have two of the following three and must be kept in mind when developing a system 
- Consistency
- Availability
- Partition tolerance 

##### How do you model data in a NoSQL database compared to a relational database?

NoSQL databases work on the idea of denormalizing the data going into a database and inserting them into a singl document or entity. This allows for having flexible data models.

##### Write a simple query to insert a document into a MongoDB collection.

		db.collection.insertOne({name: 'John Doe', age: 30, city: 'New York'})

##### How would you retrieve all documents from a specific collection in MongoDB?

		db.collection.find({})

##### Explain the concept of eventual consistency in NoSQL databases.

Eventual Consistency: Is a consistency model where eventualy all nodes will be updated with the correct information. This is to enable Distributed systems to work concurrently.


##### Write a query to update a specific field in a document in a MongoDB collection.

		db.collection.UpdateOne({name: Tim}, {$set: {age: 10} })

##### Write a query to delete a document from a MongoDB collection based on a specific condition.

		db.collection.deleteOne({name: Tim})


##### What is sharding in NoSQL databases, and why is it important?

Sharding is mothod of distrabuting data across mutiple servers to ensure scalability

Sharding helps manage large datasets by bringing them down into smaller more managable pieces

##### Write a code snippet to perform a basic aggregation operation in MongoDB.

db.collection.aggregate([{ $group: { _id: '$field', total: { $sum: 1} } }])

##### Write a query to find documents in a MongoDB collection that match a specific condition.

db.collections.find({age: { $gt: 25}})

##### Write a query to perform a join operation in a NoSQL database that supports it.

 _joins the 'orders' collection with the 'customers' collection based on the 'customerId' field."_

db.orders.aggregate({ $lookup: {from: 'Customers', localField: 'customerId', foreignField: '_id': as : 'CustomerDetails'}})