# bdsassignment2
bds assignment 2
Installation of MongoDB on Mac 
https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/

Required dataset uploaded
https://github.com/psiva1/bdsassignment2/blob/main/restaurant.json

Imported the json with the command 
mongoimport --db businessDB --collection companies --file /Users/siva_pothapragada/Documents/db/restaurant.json --jsonArray

Show databases to get list of dbs 

use <dbname>

show collections

to get list of records executed below script in mongodb terminal 

var collections = db.getCollectionNames();
for(var i = 0; i< collections.length; i++){    
   print('Collection: ' + collections[i]); // print the name of each collection
   db.getCollection(collections[i]).find().forEach(printjson); //and then print the json of each of its elements
}

to rename collection use this
db.originalCollectionName.renameCollection('newCollectionName')


for creating multi instances to analyse the read / write stats

In the terminal we need to execute the following

# Start three mongod instances:
mongod --replSet rs0 --port 27017 --dbpath /data/node1 --bind_ip localhost
mongod --replSet rs0 --port 27018 --dbpath /data/node2 --bind_ip localhost
mongod --replSet rs0 --port 27019 --dbpath /data/node3 --bind_ip localhost

mongodb terminal
setmongod --port 27017

rs.initiate({
  _id: "rs0",
  members: [
    { _id: 0, host: "localhost:27017" },
    { _id: 1, host: "localhost:27018" },
    { _id: 2, host: "localhost:27019" }
  ]
})


3. Compare the latency for different consistency levels. Generally, local settings are faster as they don't require full replication or consensus, while majority or linearizable settings might lead to higher latency due to the need for more acknowledgments and verification across multiple nodes.


In the terminal we need to execute the following

# Start three mongod instances:
mongod --replSet rs0 --port 27017 --dbpath /data/node1 --bind_ip localhost
mongod --replSet rs0 --port 27018 --dbpath /data/node2 --bind_ip localhost
mongod --replSet rs0 --port 27019 --dbpath /data/node3 --bind_ip localhost

mongodb terminal
setmongod --port 27017

rs.initiate({
  _id: "rs0",
  members: [
    { _id: 0, host: "localhost:27017" },
    { _id: 1, host: "localhost:27018" },
    { _id: 2, host: "localhost:27019" }
  ]
})

    
 

 

 









businessDB> db.collection.find({}).readConcern("majority");
[
  { _id: ObjectId('680e38b141844bf7c2f43f34'), name: 'Test Company' },
  { _id: ObjectId('680e38d641844bf7c2f43f35'), name: 'Company A' }
]
businessDB> db.collection.insertOne({ name: "Test Company" },
... { writeConcern: { w: "majority" } });
{
  acknowledged: true,
  insertedId: ObjectId('680e398341844bf7c2f43f36')
}
businessDB> db.collection.find({}).explain("executionStats");

businessDB> db.collection.insertOne({ name: "Company A" }).explain("executionStats");
TypeError: db.collection. ...  A" }).explain is not a function
businessDB> db.collection.insertOne({ name: "Test Company" }).explain("executionStats");
TypeError: db.collection. ... ny" }).explain is not a function
businessDB> db.collection.insertOne({ name: "restaurants" }).explain("executionStats");
TypeError: db.collection. ... ts" }).explain is not a function
businessDB> db.collection.insertOne({ name: "restaurant" }).explain("executionStats");
TypeError: db.collection. ... nt" }).explain is not a function
businessDB> db.testcol.insertOne({}, {writeConcern: {w:1}})
{
  acknowledged: true,
  insertedId: ObjectId('680e3a5341844bf7c2f43f3b')
}
businessDB> db.testcol.insertOne({}, {writeConcern: {w:"majority"}})
{
  acknowledged: true,
  insertedId: ObjectId('680e3a6141844bf7c2f43f3c')
}
businessDB> db.getMongo().setReadConcern("local")

businessDB> db.getMongo().setReadConcern("majority")

businessDB> db.collection.find({}).explain("executionStats");
