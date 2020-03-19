# build jar file
mvn clean install -DskipTests

# Start by docker-compose
docker-compose up -d

# Start by deploying into Stack
docker stack deploy -c docker-compose-spring-rest-api-stack.yml spring-rest-stack

# The app will start running at http://localhost:8080.

# Explore Rest APIs
# The app defines following CRUD APIs.

GET /api/notes

POST /api/notes

GET /api/notes/{noteId}

PUT /api/notes/{noteId}

DELETE /api/notes/{noteId}
