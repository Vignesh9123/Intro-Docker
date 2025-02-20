# Networks

## The Problem it addresses

- Lets say we have a backend container and a database container.
- The backend container needs to communicate with the database container.
- The database container is running on port 27017 and the backend container is running on port 3000 and both are port mapped
- If the backend code specifies localhost:27017 as the database host, it will not be able to connect to the database container as the database container is running on a different network.
- This is because each container has its own network stack , file system, etc and localhost refers to the container itself.
- Thus the backend container's localhost is different from the database container's localhost. Thus the localhost specified in the backend code does not mean the localhost of the database container or the host machine.It means the localhost of the backend container itself.
- As there is no database container running on the backend container's localhost:27017, the backend container will not be able to connect to the database container.

## Solution

- To solve this problem, we need to create a network and attach both the backend and database containers to this network.
- This way both the backend and database containers can communicate with each other using the container names as the host.

```sh
docker network create my-network
```

```sh
# Here we are attaching the mongo container to the network my-network
# Here the --name flag is used to specify the name of the container and this name can be used to refer to the mongo container in the network.
# It is a good practice to specify the name of the container as it makes it easier to refer to the container in the network.
docker run -d -p 27017:27017 --v my-mongo-data:/data/db  --network my-network --name mongodb1 mongo
```

```sh
# Here we are attaching the backend container to the network my-network
# Here the requirement of name is not that important as we are not going to refer to the backend container in any other container in the network(usually).
docker run -d -p 3000:3000 --network my-network backend
```

- Now the backend container can communicate with the database container using the container name as the host.
Eg:
```js
// In the backend code
const mongoose = require('mongoose');
mongoose.connect('mongodb://mongodb1:27017/my-database'); // Here mongodb1 is the name of the database container and my-database is the name of the database created in mongodb.
```

- Thus by creating a network and attaching both the backend and database containers to this network, we can solve the problem of containers not being able to communicate with each other.
- This is very useful when we have multiple containers that need to communicate with each other eg backend, primary database(mongodb, postgres), secondary database/queues (redis, kafka), etc.


