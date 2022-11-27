# Docker MongoDB instructions (Football Admin Application)

Instructions for Docker instance for FootballAdmin Application

## STEPS

1. Install Docker CLI or Docker Desktop

2. Create a local dedicated folder for a Docker Volumen

Example:
```sh
mkdir ~/mongoDB/mongoVolumen
```

3. Go to the created folder
Example:
```sh
cd ~/mongoDB/mongoVolumen
```

4. Get the latest Docker Image for MongoDB
```sh
docker pull mongo:latest
```

5. Execute the following command to start the Docker Image for Mongo (Consider to use the path from the folder created and respect the name of the mongo instance 'football-admin-mongo')
```sh
docker run -it -v ~/mongoDB/mongoVolumen:/data/db -p 27017:27017 --name football-admin-mongo -d mongo
```

6. Execute the following command to enter to the Mongo CLI
```sh
docker exec -it football-admin-mongo bash
```

7. Once the Mongo CLI started execute the following command
```sh
mongosh
```

8. You will the confirmation for MongoDB and execute the following command
```sh
use football-admin-db
```

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

11. DONE!
