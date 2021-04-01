# Create MongoDB instance in a Docker Image

<img src="https://github.com/georgeous497git/dockerMongoDB/blob/main/dockerMongoDB.png" width="500" height="250">

### 1. Get MongoDB Docker Image.
```
docker pull mongo
```

### 2. Create a new folder to mount volumen to MongoDB Docker Image. For example:
```
mkdir -p ~/DockerImages/mongoDB/mongoInstanceVol
```

### 3. Execute MongoDB Docker Image following the next commands:
```
docker run -it -v ~/DockerImages/mongoDB/mongoInstanceVol:/data/db -p 27017:27017 --name mongoInstance -d mongo
```

<img src="https://github.com/georgeous497git/dockerMongoDB/blob/main/commandDockerRun.png">


##### Just explaining commands:

- **-it:** Provides an interactive shell to the Docker container.
- **-v:** Use this option to attach the **/mongoInstanceVol** host volume to the **/data/db** container volume.
- **-d:** Starts the container as a background process.
- **-p:** Set mongodb port
- **--name:** Name of the container.

### 4. Validate MongoDB Docker Image creation with the next command:
```
docker ps
```
<br/>
<img src="https://github.com/georgeous497git/dockerMongoDB/blob/main/commandDockerPs.png">

### 5. Accessing to MongoDB console:
```
docker exec -it mongoInstance bash
```
<img src="https://github.com/georgeous497git/dockerMongoDB/blob/main/commandDockerExec.png">

##### Type the command:

```
mongo
```
Imagen: docker mongo

##### 5.1 Create MongoDB Role: 

```
use yourDataBaseName

db.createRole(
{
role: "yourRoleName",
privileges: [
{ resource: { db: "yourDataBaseName", collection: "" }, actions: [ "find", "update", "insert", "remove" ] }
],
roles: []
},
{ w: "majority" , wtimeout: 5000 }
)
```

<img src="https://github.com/georgeous497git/dockerMongoDB/blob/main/mongoCreateRole.png">

##### 5.1 Create MongoDB User:
```
use yourDataBaseName

db.createUser(
{
user: "userYourDataBaseName",
pwd: "passYourDataBaseName",
roles: [{role: "yourRoleName", db: "yourDataBaseName"}]
}
)
```
<img src="https://github.com/georgeous497git/dockerMongoDB/blob/main/mongoCreateUser.png">

