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

### Response -> JSON ???

JSON -> Javascript Object Notation

JSON

Data Object - {}
Data Array - []

Data -> Key Value Pair

Key -> Always String

Value -> Can be String, Number, Boolean, Array, Object

```json
{
	"name" : "Vicky",
	"city" : "Thiruvarur",
	"pincode" : 610001,
	"isMarried": true,
	"address" : {
		"street" : "udayar Street",
		"door": "5A"
	},
	"languages": ["Tamil", "English", "Hindi"],
	"companies": [{"name": "TCS", "location": "Chennai"}, {"name": "CTS", "location": "Bengaluru"}]
}
```
## Connecting with database

**Step 1**: 

Added dependencies in pom.xml

```xml
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jdbc</artifactId>
		</dependency>

		<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>8.0.31</version>
		</dependency>
```

**Step 2**: 

In `application.properties` file, add the following

```
spring.datasource.url=jdbc:mysql://localhost:3306/itech
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

**Step 3**: 

Autowired `JDBCTemplate` in Service class

```java

@Service
public class EmployeeService {

    @Autowired
    JdbcTemplate jdbcTemplate;
}
```

**Step 4**:

To run `SELECT` query, use `jdbcTemplate.query()`. It takes 2 arguments. 1st argument is SQL SELECT QUERY, 2nd Argument is `RowMapper`

RowMapper -> This class converts JDBC Response to JAVA OBJECT. It uses ResultSet class to achieve the same

```java
 List<Employee> employeeList = jdbcTemplate.query("select * from employee", new RowMapper<Employee>() {
 	@Override
        public Employee mapRow(ResultSet rs, int rowNum) throws SQLException {
            int id = rs.getInt("id");
            String name = rs.getString("name");
            String department = rs.getString("department");
            Employee employee = new Employee(id, name, department);
            return employee;
         }
});
```

**Step 5**: 

Autowire Service class in Controller class

