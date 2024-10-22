# Backend_Advanced
# Spring Boot Actuator Notes

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
