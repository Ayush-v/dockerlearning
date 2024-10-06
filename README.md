
# Docker Compose Setup for MongoDB and Mongo Express

This Docker Compose configuration sets up two services: **MongoDB** and **Mongo Express**. MongoDB is a NoSQL database, and Mongo Express is a web-based user interface for interacting with MongoDB.

## Services

### 1. **MongoDB** Service
- **Image**: `mongo`
- **Ports**: 
  - Maps the container's port `17017` to the host's port `27017`. (Note: you might want to fix the port mapping if `27017` is the intended port for MongoDB.)
- **Environment Variables**:
  - `MONGODB_INITDB_ROOT_USERNAME`: Set to `admin`. This is the root username for MongoDB.
  - `MONGODB_INITDB_ROOT_PASSWORD`: Set to `supersecret`. This is the root password for MongoDB.

MongoDB will be accessible at `localhost:27017` from your host machine (after correcting the port mapping, if needed).

### 2. **Mongo Express** Service
- **Image**: `mongo-express`
- **Ports**: 
  - Maps the container's port `8081` to the host's port `8081`. This will allow you to access the Mongo Express web interface on `localhost:8081`.
- **Environment Variables**:
  - `ME_CONFIG_MONGODB_ADMINUSERNAME`: Set to `admin`. This is the MongoDB admin username that Mongo Express will use to authenticate.
  - `ME_CONFIG_MONGODB_ADMINPASSWORD`: Set to `supersecret`. This is the MongoDB admin password that Mongo Express will use to authenticate.
  - `ME_CONFIG_MONGODB_SERVER`: Set to `mongodb`. This specifies the hostname of the MongoDB service (the name of the service in the Docker Compose file).

Mongo Express will be accessible at `localhost:8081` from your host machine. This web interface allows you to manage your MongoDB database visually.

## Requirements

- Docker
- Docker Compose

## How to Use

1. **Clone the repository** (or create a file named `docker-compose.yml` and paste the code inside).
   
2. **Start the services**:
   Run the following command in the directory containing the `docker-compose.yml` file:

   ```bash
   docker-compose up
   ```

3. **Access the services**:
   - MongoDB will be running on port `27017` (or the correct port mapping if modified).
   - Mongo Express will be accessible on `http://localhost:8081`.

4. **Stop the services**:
   To stop and remove the containers, networks, and volumes, run:

   ```bash
   docker-compose down
   ```

## Troubleshooting

- **Port conflicts**: If port `27017` is already in use by another service, you may need to adjust the port mapping in the `docker-compose.yml` file. For example:

  ```yaml
  ports:
    - 27018:17017
  ```

- **Accessing MongoDB from another container**: The MongoDB instance is accessible by other containers within the same Docker network using the service name `mongodb`. For example:

  ```bash
  docker exec -it <container_name> mongo -u admin -p supersecret --authenticationDatabase admin
  ```

- **Logging**: You can check logs by running:

  ```bash
  docker-compose logs
 
