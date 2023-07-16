# mongodb cli

# start mongodb
C:\Program Files\MongoDB\Server\4.4\bin\mongod.exe --dbpath="c:\data\db"

# MongoDB: Create User – For Database, Admin, Root

## connect mongodb
$ mongo

## Create Admin/Root User in MongoDB
> use admin

> db.createUser(
  {
    user: "mongo-admin",
    pwd: "passw0rd",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)

> db.createUser(
  {
    user: "mongo-root",
    pwd: "passw0rd",
    roles: [ { role: "root", db: "admin" } ]
  }
)

## Create User For Database
> use my-database

> db.createUser(
  {
    user: "my-user",
    pwd: "passw0rd",
    roles: [ { role: "readWrite", db: "my-database" } ]
  }
)

> db.createUser(
  {
    user: "my-user",
    pwd: "passw0rd",
    roles: [ 
             { role: "readWrite", db: "my-database" },
             { role: "read", db:"another-database" }
           ]
  }
)

## show mongodb users
> db.getUsers()
> show users

## delete users
> db.dropUser("my-user")

# some commands
use myNewDatabase
db.myCollection.insertOne( { x: 1 } );
db.myCollection.find().pretty()
quit() # or <ctrl-d>