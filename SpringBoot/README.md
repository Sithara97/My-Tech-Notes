#  SpringBoot Notes
## Setup
* Go to https://start.spring.io/
* Choose Maven
* Choose language as **Java**
* Choose version as **2.7.7**
* Group - Package Name (name of website in reverse)
* Artifact - Name (output of the project)
* Dependency - Spring Web
* Packing - jar
* Java version - 11 or 8
* Click Generate

## Run via Ngrok

To Expose your application temporarily to outside world

```
> ngrok http 8080
```

## Understand the concept

Spring Boot helps you create Web Application. Application will run in Tomcat Server by default

Communication between Server & Client -> HTTP Request

HTTP Request -> will/should followed by a HTTP Response

HTTP Request -> HEADER (Optional), BODY (Optional), URL (Mandatory)
HTTP Reponse -> HEADER (Optional), BODY (Optional), HTTP STATUS (Mandatory)

### Website vs WebService

Website -> HTTP Request -> HTTP Response -> Content-Type -> text/html -> Website

WebService/Web API -> HTTP Request -> HTTP Response -> Content-Type -> application/json -> WebService
