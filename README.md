# MongoDB-for-RDBMS-Developers

## MongoDB

It is a NOSQL Document based Database. Where all entries stored in documnent in json format.

## MongoDB Characterstics

1. **Speed**

2. **Ease of Use.**

3. **Store data as documents an documents in collections.**

4. **Objects starts with *'{'* and ends with *'}'***

5. **Data Stores as Key-Value Pair.**

## Instruction to download and run

We can go to official website and download zip file and extract. Create two additional folders *data*,*db* in the same directory. Run the executable from bin first **mongod.exe** and then **mongo.exe**.

## Basic queries for MongoDB

1. **Show dbs**:- It will show all the DBs present currently.

2. **use mydb**:-Create mydb if not exist and switch to mydb.

3. **db.createCollections('friends')**:-Create a collection named *'friends'*.

4. **db.friends.insert({name:"john",age:23})**:-insert Document(record) in collection *friends*.

5. **db.friends.find()**:- return all the enteries from the collection friends.

6. **db.friends.insert({name:"Mary",age:25})**:- Insert the document({name:"Mary",age:25}) into friends collection.

7. **db.friends.find({name:"john"})**:- it will return all document where name is *john*.

8. **db.friends.find({age:23})**:- return all documents in friends collection with age 23.

9. **db.friends.find({},{name:1})**:- Return all the documents as filter condition is ({}). Data will be returned _id , name field as fields to return specify as ({name:1}). By default _id will be returned. To remove _id from the result we have to write **db.friends.find({},{name:1,_id=0})**. For including the field keep 1 for excluding 0.

10. **db.friends.find({},{age:1,_id:0}).sort(age:1)**:- It will sort the returned records with age Ascending order. To sort it descending we can use *.sort(age:-1)*.

11. **db.friends.find().Limit(1)**:- It will return only one record/document from friends collection.

## Update Documents in MongoDB

1. ```db.friends.update({},{$set:{gender:"m"}})```:- It will update the by default one document. First parameter in update is filter criteria which is blank, should have multiple records but to update multiple document. We explicitly has to specify **db.friends.update({},{$set:{gender:"m"}},{multi="true"})**

2. ```db.friends.update({name:"Mary"},{$set:{gender:"f"}})```:-It will update only record for Mary.

3. ```db.friends.update({},{$unset:{gender=""}},{multi="true"})```:- It will remove the column gender from all the documents as multi is true. If we haven't used multi then only one record/document will be updated.

4. ```db.friends.update({name:"john"},{name:"John2",favouritefood:"indian"})```:- it will update the document for john to john2.

5. ```db.friends.remove({name:"john2"})```:- It woll only remove document for john2.

6. ```db.friends.remove()```:- It will remove all the documents present in friends collection.

7. ```db.friends.drop()```:- It will drop the collection friends from DB.

## Document Relationships

1. One to One(1:1)

2. One to Many(1:N)

3. Many to Many(N:N)

## Indexing

To increatse the Speed of Data retrieval we need to create indexing on collections.

1. ```db.comments.ensureIndex({author:1})```:- It is creating index on comments collecton on athor column ascending order. It is drpricated now, In place of ensureIndex we should use createIndex()

2. ```db.comments.getIndex()```:- It will return all indexes present on comments collection.

3. ```db.comments.dropIndex("author_1")```:- Get the name from db.comments.getIndex() and use here to drop that index on comments collection.

### Use Case of Indexing

we have a collection comments with the following structure.

```console
{
    {"_id":,
     "author":,
     "body": ,
     "upvotes":,
     "tags":
     },
     ...
}
```

> **db.comments.ensureIndex({"body":"text"})**

> **```db.comments.find({$text:{$search:"MongoDB"}})```**

It will find all the collection which has *MongoDB* Keyword in body text of collection.
