# Backend_Advanced

## Actuator

Spring Boot Actuator provides production-ready features to help you monitor and manage your Spring Boot application.

## 1. Adding Actuator Dependency

To use Actuator, add the following dependency to your project.

### Maven (`pom.xml`):

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```
## 2. Configuring Actuator
- management.endpoints.web.exposure.include=*
- management.endpoint.health.show-details=always


## 3. Accessing Actuator Endpoints

Once the Actuator is enabled, the following endpoints can be accessed by default:

- **Health Check**: [http://localhost:8080/actuator/health](http://localhost:8080/actuator/health)
- **Metrics**: [http://localhost:8080/actuator/metrics](http://localhost:8080/actuator/metrics)
- **Info**: [http://localhost:8080/actuator/info](http://localhost:8080/actuator/info)
- **Environment**: [http://localhost:8080/actuator/env](http://localhost:8080/actuator/env)
- **Beans**: [http://localhost:8080/actuator/beans](http://localhost:8080/actuator/beans)

> Replace `localhost:8080` with your actual server address and port.

## 4 Customize End Points

- management.endpoints.web.exposure.include=health,info
- management.endpoints.web.exposure.exclude=env

## 5. Common Actuator Endpoints
- **/actuator/health:**  Shows the health status of the application.
- **/actuator/metrics:** Displays various metrics (CPU, memory usage, etc.).
- **/actuator/info:**    Provides general application information (can be customized).
- **/actuator/env:**     Displays environment properties.
- **/actuator/beans:**   Shows all Spring beans loaded in the application.
- **/actuator/loggers:** Allows viewing and configuring log levels dynamically.


## Validation

Spring Boot provides a powerful validation mechanism to ensure data integrity by using annotations. Below are key concepts and steps for implementing validation in Spring Boot.

### 1. Adding Validation Dependency

To enable validation in Spring Boot, you need to add the Hibernate Validator dependency, as it’s the reference implementation of Bean Validation.

### Maven (`pom.xml`):

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```
### 2. Common Validation Annotations
Here are some commonly used validation annotations in Spring Boot:

- **@NotNull:** Ensures that the field is not null.
- **@NotEmpty:** Ensures that the field is not empty (for collections, strings, etc.).
- **@NotBlank:** Ensures that the field is not blank (applies to strings).
- **@Size(min, max):** Validates that the field’s size is between the specified bounds.
- **@Min(value):** Ensures the numeric field has a minimum value.
- **@Max(value):** Ensures the numeric field has a maximum value.
- **@Pattern(regex):** Validates that the field matches a regular expression.
- **@Email:** Validates that the field is a valid email address.

> Example Code With Implementing Validations
```java
import jakarta.validation.constraints.*;

public class User {
    
    @NotNull(message = "Name is required")
    private String name;
    
    @Size(min = 6, max = 20, message = "Username must be between 6 and 20 characters")
    private String username;

    @Email(message = "Email should be valid")
    private String email;

    @Min(value = 18, message = "Age should not be less than 18")
    private int age;
    
    @Pattern(regexp = "^[a-zA-Z0-9]*$", 
             message = "Password must only contain alphanumeric characters.")
    private String password;
    
    // Getters and setters
}
```
> Handling Validations in Controller

```java
import org.springframework.validation.annotation.Validated;
import org.springframework.web.bind.annotation.*;
import jakarta.validation.Valid;
import org.springframework.http.ResponseEntity;

@RestController
@RequestMapping("/api/users")
public class UserController {

    @PostMapping
    public ResponseEntity<String> createUser(@Valid @RequestBody User user) {
        // Handle user creation
        return ResponseEntity.ok("User created successfully");
    }
}
```
## Scheduler

- Configuration for POM.XML
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
</dependency>
```
- Service class Configurations

```java
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Service;

import java.time.LocalDateTime;

@Service
public class MovieService {

    // Method to report current time every 5 seconds
    @Scheduled(fixedRate = 5000)
    public void reportCurrentTime() {
        System.out.println("Current time: " + LocalDateTime.now());
    }

    // Example of another scheduled task
    @Scheduled(cron = "0 0 12 * * ?") // Every day at noon
    public void scheduledTask() {
        System.out.println("Scheduled task running at noon");
    }
}
```
# Types of Schedules

- **Fixed Rate**
  ```java
  @Scheduled(fixedRate = 5000) // Executes every 5 seconds
  public void fixedRateTask() {
      // Task logic here
  }
```
