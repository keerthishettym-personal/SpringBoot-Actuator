# Spring Boot Actuator Demo Application

## Overview

This project is a **medium-level Spring Boot application** created to demonstrate **Spring Boot Actuator** features to an audience ranging from **beginners to experienced developers**. The application showcases how Actuator helps in **monitoring, managing, and observing** Spring Boot applications in production-like environments.

The project uses **H2** as the database and exposes commonly used Actuator endpoints with proper configuration and examples.

---

## What is Spring Boot Actuator?

Spring Boot Actuator provides **production-ready features** that help you monitor and manage your application. It exposes various **endpoints** over HTTP or JMX to check application health, metrics, environment details, and more.

Actuator is essential for:

- Production monitoring
- DevOps & SRE practices
- Microservices observability
- Troubleshooting and diagnostics

---

## Tech Stack

- Java 17+
- Spring Boot
- Spring Boot Actuator
- Spring Data JPA
- PostgreSQL
- Maven

---

## Core Actuator Features Demonstrated

### Health Checks

- Monitor application health in real time
- Includes database connectivity status
- Custom health indicators (optional extension)

Endpoint:

```
/actuator/health
```

---

### Metrics

- JVM metrics (memory, GC, threads)
- HTTP request metrics
- Custom application metrics

Endpoint:

```
/actuator/metrics
```

Example:

```
/actuator/metrics/jvm.memory.used
```

---

### Info Endpoint

Displays custom application metadata.

Endpoint:

```
/actuator/info
```

Example configuration:

```properties
info.app.name=Spring Boot Actuator Demo
info.app.description=Demo application for monitoring and management
info.app.version=1.0.0
```

---

### Environment & Configuration

- View active profiles
- Inspect environment properties (controlled exposure)

Endpoint:

```
/actuator/env
```

---

### Beans & Mappings

- View loaded Spring beans
- Inspect request mappings

Endpoints:

```
/actuator/beans
/actuator/mappings
```

---

## Database Configuration (PostgreSQL)

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/actuator_demo
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

Database health is automatically reflected in:

```
/actuator/health
```

---

## Database Configuration (H2)

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
```

Database health is automatically reflected in:

```
/actuator/health
```

---

## Actuator Configuration

```properties
management.endpoints.web.exposure.include=health,info,metrics,env,beans,mappings
management.endpoint.health.show-details=always
management.endpoints.web.base-path=/actuator
```

> ⚠️ In production, avoid exposing sensitive endpoints publicly.

---

## Security Considerations (Good to Have)

- Secure Actuator endpoints using **Spring Security**
- Expose only required endpoints
- Restrict access by role (e.g., ADMIN)

Example:

- `/actuator/health` → public
- `/actuator/**` → admin-only

---

## Running the Application

```bash
mvn clean install
mvn spring-boot:run
```

Application runs at:

```
http://localhost:8080
```

Actuator base path:

```
http://localhost:8080/actuator
```

---

## Common Issues & Tips

- `/actuator/info` shows `{}` → Ensure `info.*` properties are defined
- PostgreSQL DOWN → Health endpoint reports `DOWN`
- Too many endpoints exposed → Limit via configuration

---

## Learning Outcomes

- Understand what Actuator is and why it matters
- Learn commonly used production endpoints
- Gain insight into real-world monitoring practices
- Prepare for DevOps and microservices environments

---

## Future Enhancements

- Add Prometheus & Grafana integration
- Custom health indicators
- Distributed tracing (Zipkin / OpenTelemetry)
- Dockerize the application

## License

This project is for learning and demo purposes.
