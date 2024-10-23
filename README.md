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

## Lombok

### Maven
```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.26</version> <!-- or the latest version -->
    <scope>provided</scope>
</dependency>
```
## Annotations of Lombok

## Lombok Annotations

Lombok is a Java library that helps reduce boilerplate code by automatically generating common methods like getters, setters, constructors, etc. Below is a summary of key Lombok annotations, their purposes, and usage examples.

### 1. `@Data`
- **Purpose**: A convenient shorthand that bundles the functionalities of several annotations: `@Getter`, `@Setter`, `@ToString`, `@EqualsAndHashCode`, and `@RequiredArgsConstructor`.
- **Usage**:
    ```java
    import lombok.Data;

    @Data
    public class User {
        private String name;
        private int age;
    }
    ```

### 2. `@Getter`
- **Purpose**: Automatically generates getter methods for the fields of the class.
- **Usage**:
    ```java
    import lombok.Getter;

    public class User {
        @Getter
        private String name;
    }
    ```

### 3. `@Setter`
- **Purpose**: Automatically generates setter methods for the fields of the class.
- **Usage**:
    ```java
    import lombok.Setter;

    public class User {
        @Setter
        private String name;
    }
    ```

### 4. `@ToString`
- **Purpose**: Generates a `toString()` method that returns a string representation of the object, including all fields.
- **Usage**:
    ```java
    import lombok.ToString;

    @ToString
    public class User {
        private String name;
        private int age;
    }
    ```

### 5. `@EqualsAndHashCode`
- **Purpose**: Generates `equals()` and `hashCode()` methods based on the fields of the class.
- **Usage**:
    ```java
    import lombok.EqualsAndHashCode;

    @EqualsAndHashCode
    public class User {
        private String name;
        private int age;
    }
    ```

### 6. `@NoArgsConstructor`
- **Purpose**: Generates a constructor with no parameters.
- **Usage**:
    ```java
    import lombok.NoArgsConstructor;

    @NoArgsConstructor
    public class User {
        private String name;
    }
    ```

### 7. `@AllArgsConstructor`
- **Purpose**: Generates a constructor with one parameter for each field in the class.
- **Usage**:
    ```java
    import lombok.AllArgsConstructor;

    @AllArgsConstructor
    public class User {
        private String name;
        private int age;
    }
    ```

### 8. `@RequiredArgsConstructor`
- **Purpose**: Generates a constructor for all final fields and fields marked with `@NonNull`.
- **Usage**:
    ```java
    import lombok.RequiredArgsConstructor;
    import lombok.NonNull;

    @RequiredArgsConstructor
    public class User {
        private final Long id; // Must be initialized
        @NonNull
        private String name; // Cannot be null
    }
    ```

###  9. `@NonNull`
- **Purpose**: Indicates that a field should not be null. Lombok will add a null check in the generated constructor or setter methods.
- **Usage**:
    ```java
    import lombok.NonNull;

    public class User {
        @NonNull
        private String name; // Will throw NullPointerException if null
    }
    ```

###  10. `@Slf4j`
- **Purpose**: Provides a logger instance (`log`) for the class, enabling easy logging.
- **Usage**:
    ```java
    import lombok.extern.slf4j.Slf4j;

    @Slf4j
    public class User {
        public void logDetails() {
            log.info("User details");
        }
    }
    ```
- Example COde By Including All Lombok Annotations
  ```java
  import lombok.Data;
    import lombok.NoArgsConstructor;
    import lombok.AllArgsConstructor;
    import lombok.RequiredArgsConstructor;
    import lombok.NonNull;
    
    @Data // Generates getters, setters, toString, equals, and hashCode
    @NoArgsConstructor // Generates a no-arguments constructor
    @AllArgsConstructor // Generates a constructor with all fields
    @RequiredArgsConstructor // Generates a constructor for final and @NonNull fields
        public class User {

    private final Long id; // This field is final
    @NonNull
    private String name; // This field is non-null

    private String email;
    private int age;

    // Main method for testing
    public static void main(String[] args) {
        // Using @RequiredArgsConstructor-generated constructor (id is final, name is @NonNull)
        User user = new User(1L, "John Doe");

        // Testing the generated toString() method
        System.out.println(user);

        // Using the all-args constructor
        User fullUser = new User(2L, "Jane Doe", "jane.doe@example.com", 30);
        System.out.println(fullUser);

        // Testing equals and hashCode
        System.out.println("Users equal: " + user.equals(fullUser));
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
## Service class Configurations

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
## Configuration of Application Class
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.scheduling.annotation.EnableScheduling;

@SpringBootApplication
@EnableScheduling
public class SchedulingApplication {

    public static void main(String[] args) {
        SpringApplication.run(SchedulingApplication.class, args);
    }
}
```

## Types of Schedules

**Fixed Rate**
  ```java
  
  @Scheduled(fixedRate = 5000) // Executes every 5 seconds
  public void fixedRateTask() {
      // Task logic here
  }
  ```
- Runs the task at a fixed interval, starting the next execution as soon as the interval is reached, regardless of when the previous task finished.

**Fixed Delay**
 ```java
    @Scheduled(fixedDelay = 3000) // Executes 3 seconds after the last execution finishes
         public void fixedDelayTask() {
        // Task logic here
    }

  ```
 - Runs the task with a delay between the completion of the last execution and the start of the next one.

**Initial Delay**
```java
@Component
public class InitialDelayTask {

    @Scheduled(fixedRate = 5000, initialDelay = 10000) // Start after 10 seconds
    public void runTaskWithInitialDelay() {
        System.out.println("Task running with initial delay - " + System.currentTimeMillis());
    }
}
```
**Cron Expression**
```java
@Component
public class CronTask {

    @Scheduled(cron = "0 0 * * * *") // Runs at the start of every hour
    public void runTaskWithCron() {
        System.out.println("Task running on the hour - " + System.currentTimeMillis());
    }
}
```
## Cache

The `@Cacheable` annotation is part of the Spring Framework's caching abstraction. It is used to indicate that the result of a method can be cached, thus improving performance by avoiding unnecessary computations for the same inputs.

### Purpose
- **Caching Results**: `@Cacheable` helps store the result of method invocations, so subsequent calls with the same parameters can return the cached result instead of executing the method again.
- **Performance Improvement**: By caching frequently accessed data, applications can reduce latency and decrease load on resources.

### Usage
The `@Cacheable` annotation can be applied to methods, and it accepts several attributes to customize its behavior:

- **value**: Specifies the name of the cache(s) to use.
- **key**: Defines a custom key for the cached value.
- **condition**: A SpEL expression to specify whether the method result should be cached.
- **unless**: A SpEL expression to specify whether the method result should not be cached.
- **keyGenerator**: Specifies a custom key generator.

### Example

### Service Class with `@Cacheable`

Here’s an example of a service class that uses the `@Cacheable` annotation:

```java
import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Service;

@Service
public class MovieService {

    private final MovieRepository movieRepository;

    public MovieService(MovieRepository movieRepository) {
        this.movieRepository = movieRepository;
    }

    @Cacheable(value = "movies", key = "#name")
    public Movie findByName(String name) {
        return movieRepository.findByName(name);
    }
}
