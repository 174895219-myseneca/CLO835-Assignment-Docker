Setting Up a MySQL Database with Docker on Amazon EC2

This guide outlines the steps to configure and launch a MySQL database container on an Amazon EC2 instance using Docker.

Prerequisites:

    An Amazon EC2 instance with Amazon Linux.
    Administrative access to the EC2 instance.

Instructions:
Verify Docker service status: (Note: Docker has already been installed and user has been added to Docker group using custom data <custom data>.)

    ```
    systemctl status docker

    ```

Login to Amazon ECR (replace us-east-1 with your region):
```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin

```

Create Docker network:
```Bash

docker network create -d bridge --subnet .../24 --gateway <IPAdrress> new-network
```

Launch MySQL container (replace "pw" with a strong password):
```Bash
docker run --network new-network -d -e MYSQL_ROOT_PASSWORD=pw --name my_sql_db <your_db_uri>
```


List running containers:
```Bash
docker ps
```

# Running 2 tier web application using ECR

### Running mysql
```docker run --network new-network -d -e MYSQL_ROOT_PASSWORD=pw --name my_sql_db <your_db_uri>```

### Get the IP of the database and export it as DBHOST variable
```docker inspect <container_id>```

### Example when running DB runs as a docker container and app is running locally
```
export DBHOST=172.17.0.2
export DBPORT=3306
export DBUSER=root
export DATABASE=employees
export DBPWD=pw
export APP_COLOR=blue
```
### Run the application, make sure it is visible in the browser
```docker run -p 8081:8080 --network new-network  -e APP_COLOR=blue -e DBHOST=$DBHOST -e DBPWD=$DBPWD -e DBPORT=$DBPORT -e DBUSER=$DBUSER --name blue --link my_sql_db:mysql_db -d <your_webapp_uri>```
