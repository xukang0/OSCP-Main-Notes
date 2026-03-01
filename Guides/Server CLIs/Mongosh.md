cd mongosh-2.3.2-linux-x64/bin

./mongosh mongodb://{target_IP}:27017
	Connect to Mongosh server

show dbs
	show database

use [collection_name]

show collections

db.flag.find().pretty();