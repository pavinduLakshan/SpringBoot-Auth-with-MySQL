# spring-boot-auth-template
Spring Boot Authentication and authorization boilerplate with MySQL

This is a bolilerplate of Authentication and Authorization implementation with Spring Security and MySQL. 
Using this template, you will be able to jump straight into developing business logic in your Spring Boot app without focusing much about authentication details.

## How to use

1. Create new repository from this template.
2. Clone the newly created repository.

3. Initialize MySQL database

Run the following command to quickly spin up a MySQL database using Docker.

```bash
docker run -d --name "<your_container_name>" -e MYSQL_ROOT_PASSWORD="root" -p 3306:3306 mysql:latest
```

Take note of the container ID that this command outputs.

Now ssh into the docker container and create database.

```bash
docker exec -it "<your_container_id>" bash
mysql -u root -p
create database <your_database_name>;
use <your_database_name>;
```

4. Update `application.properties` with your database configurations.

5. Start the server.

```bash
sh mvnw spring-boot:run
```

## API

- Signup

Once the server is up and running, try sending a POST request to the /signup endpoint to register a user.

```curl
 curl -H 'Content-Type: application/json' \
    -d '{
    "name":"John",
    "username":"johndoe",
    "email": "johndoe@example.com", 
    "password": "JohnDoe@Test123"
    }' \
    -X POST \
    http://localhost:8080/api/auth/signup
```

This request will return a response similar to follows.

```json
{
    "success":true,
    "message":"User registered successfully"
}
```

- Login

Use `/signin` endpoint to sign in (login) to the application. Upon successful credential submission, the server will return a 200 response.

```curl
 curl -H 'Content-Type: application/json' \
    -d '{
    "usernameOrEmail":"johndoe",
    "password": "JohnDoe@Test123"
    }' \
    -X POST \
    http://localhost:8080/api/auth/signin
```

This will return a response similar to follows.

```json
{
    "accessToken":"eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIxIiwiaWF0IjoxNzExODI1MzM5LCJleHAiOjE3MTI0MzAxMzl9.Eqla98sv3rDzJtYqCHJFHvrEpLK6iwjJS68jtXYI68nJC5KIeAFq5-FaQKveTljpO-_DxEpH4rdw8zxXx0FxLg","tokenType":"Bearer"
}
```