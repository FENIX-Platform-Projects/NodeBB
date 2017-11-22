
# Prerequisites
node >= v6
npm >= 3

# Permissions on mongodb

# 1) Create an admin user (not the nodebb user)
#This user is scoped to the admin database to manage MongoDB once authorization has been enabled.

$ mongo
> db.createUser( { user: "gift_user", pwd: "gift_$2018", roles: [ { role: "readWriteAnyDatabase", db: "admin" }, { role: "userAdminAnyDatabase", db: "admin" } ] } )

> use nodebb

> db.createUser( { user: "nodebb", pwd: "gift_$2018", roles: [ { role: "readWrite", db: "nodebb" }, { role: "clusterMonitor", db: "admin" } ] } )

> quit()

#Enable database authorization in the MongoDB configuration file /etc/mongod.conf by uncommenting the line security and enabling authorization:

security:
  authorization: enabled

$ sudo service mongod restart
$ mongo -u your_username -p your_password --authenticationDatabase=admin



#SETTINGS PLUGINS

# 1) write api

$ npm install nodebb-plugin-write-api
$ sudo npm i -g npm

# update the schema
folderNodeBB>$ ./nodebb upgrade


# insert admin user
folderNodeBB>$./nodebb setup


folderNodeBB>$./nodebb activate nodebb-plugin-write-api

