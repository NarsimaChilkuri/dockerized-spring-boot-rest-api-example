# build jar file
mvn clean install -DskipTests

# Start by docker-compose
docker-compose up -d

# Start by deploying into Stack
docker stack deploy -c docker-compose-spring-rest-api-stack.yml spring-rest-stack

# Deploying in Kubernetes
kubectl apply -f k8s-resources/.

# Deploying by helm chart
helm install -g helm-chart/.

# The app will start running at http://localhost:8080.

# Explore Rest APIs
# The app defines following CRUD APIs.

GET /api/notes

POST /api/notes

GET /api/notes/{noteId}

PUT /api/notes/{noteId}

DELETE /api/notes/{noteId}


# Flyway DB Migration

# dependency changes in pom.xml

<dependency>
   <groupId>org.flywaydb</groupId>
   <artifactId>flyway-core</artifactId>
</dependency>
<dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId> 
   <scope>runtime</scope>
</dependency>


# adding properties of DB using application.properties

spring.datasource.url = jdbc:mysql://REMOTE_HOST:3306/DB_NAME
spring.datasource.username = username
spring.datasource.password = password


spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5InnoDBDialect

spring.jpa.hibernate.ddl-auto = update


# Adding Migrations in src/main/resources/db/migration

V1__init.sql 

CREATE TABLE users (
  id bigint(20) NOT NULL AUTO_INCREMENT,
  username varchar(100) NOT NULL,
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


# Build custom sonar image using dockerfile-custom-sonar

docker build -t <custom_sonar_qube_image_name> -f dockerfile-custom-sonar .


# Start SonarQube Container using custom image of SonarQube you Created

docker run -d -p 9000:9000 <custom_sonar_qube_image_name>

Create a webhook in SonarQube pointing to JENKINS HOST




# Start nexus repo manager

docker run -d -p 8081:8081 -p 8083:8083 --name nexus  sonatype/nexus3

Create a docker private repo in nexus repo manager

# Steps for docker to allowing insecure registry

Create an HTTP connector at specified port (another port where nexus container will be listening). Normally used if the server is behind a secure proxy.

Check this option "Allow clients to use the V1 API to interact with this repository"

Add insecure registry server host in docker config (/etc/docker/daemon.json)

{
  "insecure-registries" : ["HOST_IP:ANOTHER_PORT_FOR_NEXUS_LISTENING"]
}

Restart docker service

"service docker restart"





