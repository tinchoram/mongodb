# Migrate Data Tools

You can use this tools for bring data and migrate.

 - [mongorestore](https://docs.atlas.mongodb.com/import/mongorestore/): Tool for create backup and restore.
 - [mongoimport](https://docs.atlas.mongodb.com/import/mongoimport/): Tool for Load data from a `JSON` or a `CSV` file

## [mongorestore](https://docs.mongodb.com/database-tools/mongorestore/#mongodb-binary-bin.mongorestore)

You can use **mongodump** and **mongorestore** for build backup and restore on new instance.

Example: for this example I use database of [restaurants](https://docs.atlas.mongodb.com/sample-data/sample-restaurants/#std-label-restaurants-restaurants) running on instance of MongoDB server version: 4.4.6.

    > show dbs
	admin           0.000GB
	config          0.000GB
	db_restaurants  0.004GB
	local           0.000GB
	
	> use db_restaurants
	switched to db db_restaurants
	
	> db.restaurants.count()
	25359
	>
 1- Create backup with **[mongodump](https://docs.mongodb.com/database-tools/mongodump/#mongodb-binary-bin.mongodump)**: on a terminal exec

    # mongodump --db db_restaurants --out ./backups/

    Out:
    ./backups/db_restaurants/
	    - restaurants.metadata.json
	    - restaurants.bson

2 - Restore backup with **[mongorestore](https://docs.mongodb.com/database-tools/mongorestore/#mongodb-binary-bin.mongorestore)**
In a new instance of MongoDB server version: 4.4.6 

    > show dbs
	admin   0.000GB
	config  0.000GB
	local   0.000GB
	>
exec in a terminal
   

     # mongorestore --db db_restaurants ./backups/db_restaurants/

    Out: connected to mongodb
    > show dbs
	admin           0.000GB
	config          0.000GB
	db_restaurants  0.004GB
	local           0.000GB
	
	> use db_restaurants
	switched to db db_restaurants
	
	> db.restaurants.count()
	25359
	>
  
## [mongoimport](https://docs.atlas.mongodb.com/import/mongoimport/)

You can use  [`mongoimport`](https://docs.mongodb.com/database-tools/mongoimport/#mongodb-binary-bin.mongoimport)  to import data from a  `JSON`  or a  `CSV`  file into  MongoDB Atlas  cluster.

Example: for this example I use JSON file from folder "data/restaurants-dataset.json"). This file is a database example of [restaurants](https://docs.atlas.mongodb.com/sample-data/sample-restaurants/#std-label-restaurants-restaurants) and instance of MongoDB server version: 4.4.6.

     > show dbs
	admin   0.000GB
	config  0.000GB
	local   0.000GB
	>
	
1 - Import JSON file with [`mongoimport`](https://docs.mongodb.com/database-tools/mongoimport/#mongodb-binary-bin.mongoimport)

In a terminal on path "data/" exec

    # mongoimport --db db_restaurants --collection restaurants --file restaurants-dataset.json

    Out: connected to mongodb
    > show dbs
	admin           0.000GB
	config          0.000GB
	db_restaurants  0.004GB
	local           0.000GB
	
	> use db_restaurants
	switched to db db_restaurants
	
	> db.restaurants.count()
	25359
	>

2 - Export data to JSON or CSV with [`mongoexport`](https://docs.mongodb.com/database-tools/mongoexport/#mongodb-binary-bin.mongoexport) 

    > show dbs
	admin           0.000GB
	config          0.000GB
	db_restaurants  0.004GB
	local           0.000GB
	
	> use db_restaurants
	switched to db db_restaurants
	
	> db.restaurants.count()
	25359
	>
exec in a terminal

    # mongoexport --db db_restaurants -c restaurants --out ./data/db_restaurants_export.json

	Out: 
	./data/
		- db_restaurants_export.json

