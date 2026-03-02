# TDSE-Project-Statement-Web-Framework-Development-for-REST-Services-and-Static-File-Management

## Project Overview

This laboratory consists of the development of a lightweight Java-based microframework capable of:

- Serving static files (HTML, CSS, JS, images)
- Defining REST services using lambda expressions
- Extracting query parameters from HTTP requests
- Building HTTP responses correctly following the HTTP/1.1 protocol

The objective of this laboratory was to transform a basic HTTP server into a modular, extensible and maintainable web framework, reinforcing knowledge of:

- HTTP protocol architecture
- Client-server communication
- Stateless design
- Routing mechanisms
- Distributed application architecture
- Software design principles

---

## Architecture

The framework was designed following separation of responsibilities principles.

### Architecture Components

```
HttpServer
├── HttpRequestParser
├── Router
│ └── RouteHandler (Functional Interface)
├── StaticFileHandler
├── HttpResponseBuilder
├── Request
├── Response
└── MicroFramework (Public API)
```


### Responsibilities

| Class | Responsibility |
|--------|----------------|
| **MicroFramework** | Public API to define routes and start the server |
| **Router** | Registers and resolves REST routes |
| **RouteHandler** | Functional interface for lambda-based route definitions |
| **Request** | Encapsulates HTTP method, path, headers and query parameters |
| **Response** | Encapsulates HTTP status, headers and body |
| **HttpRequestParser** | Parses raw HTTP requests into Request objects |
| **StaticFileHandler** | Serves static files from configured directory |
| **HttpResponseBuilder** | Builds valid HTTP/1.1 responses |
| **HttpServer** | Manages socket connections and coordinates components |

---

## Features Implemented

### REST GET Method with Lambda Support

Example:

```java
get("/hello", (req, res) -> "Hello " + req.getValues("name"));

This allows clean and expressive route definitions.

Query Parameter Extraction

Example request:

http://localhost:8080/hello?name=Pedro

Usage inside route:

req.getValues("name");

The framework parses query strings automatically.

Static File Handling

Static folder configuration:

staticfiles("webroot");

Static files are located in:

src/main/resources/webroot

Maven copies them automatically to:

target/classes/webroot

Example:

http://localhost:8080/index.html

HTTP Protocol Compliance

The framework correctly builds HTTP responses including:

Status line (HTTP/1.1 200 OK)

Date header

Server header

Content-Length

Custom headers

Proper CRLF separation
```

Example Usage
Main.java
package org.example;

import static org.example.framework.MicroFramework.*;

public class Main {

    public static void main(String[] args) {

        staticfiles("webroot");

        get("/hello", (req, res) -> {
            res.addHeader("Content-Type", "text/plain");
            return "Hello " + req.getValues("name");
        });

        get("/pi", (req, res) -> {
            res.addHeader("Content-Type", "text/plain");
            return String.valueOf(Math.PI);
        });

        start(8080);
    }
}

## Test Endpoints

After running the server:

http://localhost:8080/

http://localhost:8080/index.html

http://localhost:8080/hello?name=Pedro

http://localhost:8080/pi

### How to Run the Project

Clone Repository

git clone <repository-url>

cd <repository-name>

 Build with Maven

mvn clean install
 
Run Application

mvn exec:java -Dexec.mainClass="org.example.Main"

Or run Main.java directly from your IDE.

Project Structure

```
src
 ├── main
 │   ├── java
 │   │   └── org/example/framework
 │   │       ├── MicroFramework.java
 │   │       ├── HttpServer.java
 │   │       ├── Router.java
 │   │       ├── RouteHandler.java
 │   │       ├── Request.java
 │   │       ├── Response.java
 │   │       ├── HttpRequestParser.java
 │   │       ├── HttpResponseBuilder.java
 │   │       └── StaticFileHandler.java
 │   │
 │   └── resources
 │       └── webroot
 │           └── index.html
 ```
Concepts Reinforced

HTTP Request/Response structure

Stateless architecture

REST service design

Socket programming

Routing systems

Query string parsing

Static resource management

Modular architecture

Maven project structure

Distributed application fundamentals

Learning Outcome

This project demonstrates a deep understanding of:

The HTTP protocol

Internet architecture

Backend framework design

Distributed systems fundamentals

Clean software architecture principles

By implementing the framework from scratch, the internal behavior of modern web frameworks such as Spring Boot, Express or Spark was better understood.

### Author

Ricardo Ayala
Transformación Digital y Soluciones Empresariales (TDSE)

### Project Status

REST routes implemented
Lambda support implemented
Query parameters extraction implemented
Static files served correctly
Modular architecture
Maven structured project
Ready for GitHub submission