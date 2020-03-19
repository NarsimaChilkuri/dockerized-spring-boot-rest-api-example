# build jar file
mvn clean install -DskipTests

The app will start running at http://localhost:8080.

Explore Rest APIs
The app defines following CRUD APIs.

GET /api/notes

POST /api/notes

GET /api/notes/{noteId}

PUT /api/notes/{noteId}

DELETE /api/notes/{noteId}
