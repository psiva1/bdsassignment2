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


