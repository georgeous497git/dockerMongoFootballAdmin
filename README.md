# Docker MongoDB instructions (Football Admin Application)

Instructions for Docker instance for FootballAdmin Application

## STEPS

1. Install Docker Desktop

2. Start Docker

3. Create a dedicated local folder for a Docker Volumen

Example:
```sh
mkdir -p mongoDB/footballAdminVolumen
```

3. Validate the folder creation
Example:
```sh
ls mongoDB/footballAdminVolumen
```

4. Get the latest Docker Image for MongoDB
```sh
docker pull mongo:latest
```
<img src="https://github.com/georgeous497git/dockerMongoFootballAdmin/blob/develop/images/4-mongoPull.png" width="600" height="250">


5. Execute the following command to start the Docker Image for Mongo (**Consider to use the absolute path for the dedicated folder and use the name of the mongo instance 'football-admin-mongo'**)
```sh
docker run -it -v /Users/lambda/Revisen/mongoDB/footballAdminVolumen:/data/db -p 27017:27017 --name football-admin-mongo -d mongo
```
<img src="https://github.com/georgeous497git/dockerMongoFootballAdmin/blob/develop/images/5-CreateMongoVolumen.png" width="600" height="100">


6. Execute the following command to enter to the Mongo CLI
```sh
docker exec -it football-admin-mongo bash
```
<img src="https://github.com/georgeous497git/dockerMongoFootballAdmin/blob/develop/images/6-mongoBash.png" width="600" height="70">


7. Once the Mongo CLI started execute the following command
```sh
mongosh
```
<img src="https://github.com/georgeous497git/dockerMongoFootballAdmin/blob/develop/images/7-sheelMongoFull.png" width="600" height="350">


8. You will the confirmation for MongoDB and execute the following command
```sh
use football-admin-db
```
<img src="https://github.com/georgeous497git/dockerMongoFootballAdmin/blob/develop/images/8-useMongo.png" width="600" height="70">

9. Execute the following script within the Mongo console
```sh
db.createRole(
  {
    role: "admin",
    privileges: [
      {
        resource: { db: "football-admin-db", collection: "" },
        actions: ["find", "update", "insert", "remove"],
      },
    ],
    roles: [],
  },
  { w: "majority", wtimeout: 5000 }
)
```
<img src="https://github.com/georgeous497git/dockerMongoFootballAdmin/blob/develop/images/9-createRole.png" width="600" height="200">

10. Execute the following script within the Mongo console
```sh
db.createUser(
    {
        user: "admin1",
        pwd: "passadmin1",
        roles: [{role: "admin", db: "football-admin-db"}]
    }
)
```
<img src="https://github.com/georgeous497git/dockerMongoFootballAdmin/blob/develop/images/10-createUser.png" width="600" height="200">

11. DONE!
