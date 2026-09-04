#MongoDb Commands

##Connect to Target IP and Port Number

``` bash
./mongosh mongodb://{target_IP}:{target_port}
```
##Show List of Databases in MongDB Server

``` MongoDB
show dbs;
```

##Query Selected Database (after show dbs command)

``` MongoDB
use {database_name};
```

##List Collections in Database

```MongoDB
show {collection_name};
```
##Dump Contents of Document in Collection

```MongoDB
db.flag.find();
```