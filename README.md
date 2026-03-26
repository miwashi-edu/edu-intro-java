# edu-intro-java

## Prepare

```bash
cd ~
cd ws
cd intro-java
git add .
git commit -m "lvel-2"
```


## Instructions

```bash
cd ~
cd ws
cd intro-java
rm -rf /app/src/main/resources/static # Remove static html
```

### ./src/main/java/net/miwashi/AuthController.java

```bash
cat > ./src/main/java/net/miwashi/AuthController.java << 'EOF'
package net.miwashi.controllers;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/auth")
public class AuthController {

    @PostMapping("/login")
    public String login() {
        return "login successful";
    }

    @PostMapping("/refresh")
    public String refresh() {
        return "refresh successful";
    }
}
EOF
```

### ./src/main/java/net/miwashi/RedirectController.java

```bash
cat > ./src/main/java/net/miwashi/RedirectController.java << 'EOF'
package net.miwashi.controllers;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class RedirectController {

    @GetMapping("/")
    public String redirectToSwagger() {
        return "redirect:/swagger-ui.html";
    }
}
EOF
```

### New Dependencies

```groovy
dependencies {
  implementation 'org.springframework.boot:spring-boot-starter-actuator'
  implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.1.0'
}
```

### ./app/src/main/resources/application.properties 

```bash
cat > ./app/src/main/resources/application.propertie << 'EOF'
spring.profiles.active=${ENV:prod}
server.port=${PORT:8080}
springdoc.api-docs.enabled=false
springdoc.swagger-ui.enabled=false
spring.devtools.restart.enabled=false
management.endpoints.web.exposure.include=health
EOF
```

### ./app/src/main/resources/application-dev.properties 

```bash
cat > ./app/src/main/resources/application-dev.properties  << 'EOF'
spring.devtools.restart.enabled=true
management.endpoints.web.exposure.include=*
springdoc.api-docs.enabled=true
springdoc.swagger-ui.enabled=true
EOF
```
### ./app/src/main/resources/application-stage.properties 

```bash
cat > ./app/src/main/resources/application-stage.properties << 'EOF'
spring.devtools.restart.enabled=true
management.endpoints.web.exposure.include=*
springdoc.api-docs.enabled=true
springdoc.swagger-ui.enabled=true
EOF
```

## Repeat

```bash
git reset --hard
git clean -df
```

## Test it

```bash
# ─── APP ────────────────────────────────────────────────────────────────────

curl -X POST http://localhost:8080/auth/login -H "Content-Type: application/json" -d '{"username": "admin", "password": "password"}'
curl http://localhost:8080/auth/refresh

# ─── API ────────────────────────────────────────────────────────────────────

# OpenAPI spec
curl http://localhost:8080/v3/api-docs
curl http://localhost:8080/v3/api-docs.yaml

# Swagger UI (returns HTML)
curl http://localhost:8080/swagger-ui.html
curl http://localhost:8080/swagger-ui/index.html

# ─── DISCOVERY ───────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator
curl http://localhost:8080/actuator/ -H "Accept: application/json"

# ─── HEALTH ──────────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/health
curl http://localhost:8080/actuator/health/liveness
curl http://localhost:8080/actuator/health/readiness
curl http://localhost:8080/actuator/health/db
curl http://localhost:8080/actuator/health/diskSpace
curl http://localhost:8080/actuator/health/redis
curl http://localhost:8080/actuator/health/rabbit
curl http://localhost:8080/actuator/health/kafka

# ─── INFO ────────────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/info

# ─── METRICS ─────────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/metrics
curl http://localhost:8080/actuator/metrics/jvm.memory.used
curl http://localhost:8080/actuator/metrics/jvm.memory.max
curl http://localhost:8080/actuator/metrics/jvm.gc.pause
curl http://localhost:8080/actuator/metrics/jvm.threads.live
curl http://localhost:8080/actuator/metrics/jvm.threads.daemon
curl http://localhost:8080/actuator/metrics/jvm.classes.loaded
curl http://localhost:8080/actuator/metrics/jvm.heap.used
curl http://localhost:8080/actuator/metrics/process.cpu.usage
curl http://localhost:8080/actuator/metrics/process.uptime
curl http://localhost:8080/actuator/metrics/process.start.time
curl http://localhost:8080/actuator/metrics/system.cpu.usage
curl http://localhost:8080/actuator/metrics/system.cpu.count
curl http://localhost:8080/actuator/metrics/http.server.requests
curl http://localhost:8080/actuator/metrics/http.server.requests?tag=status:200
curl http://localhost:8080/actuator/metrics/http.server.requests?tag=method:GET
curl http://localhost:8080/actuator/metrics/http.server.requests?tag=uri:/actuator/health
curl http://localhost:8080/actuator/metrics/hikaricp.connections
curl http://localhost:8080/actuator/metrics/hikaricp.connections.active
curl http://localhost:8080/actuator/metrics/hikaricp.connections.idle
curl http://localhost:8080/actuator/metrics/hikaricp.connections.pending
curl http://localhost:8080/actuator/metrics/cache.gets
curl http://localhost:8080/actuator/metrics/cache.puts
curl http://localhost:8080/actuator/metrics/disk.free
curl http://localhost:8080/actuator/metrics/disk.total
curl http://localhost:8080/actuator/metrics/tomcat.threads.busy
curl http://localhost:8080/actuator/metrics/tomcat.threads.current
curl http://localhost:8080/actuator/metrics/tomcat.sessions.active.current
curl http://localhost:8080/actuator/metrics/tomcat.sessions.created
curl http://localhost:8080/actuator/metrics/tomcat.global.request.max
curl http://localhost:8080/actuator/metrics/logback.events?tag=level:error
curl http://localhost:8080/actuator/metrics/logback.events?tag=level:warn
curl http://localhost:8080/actuator/metrics/logback.events?tag=level:info
curl http://localhost:8080/actuator/metrics/spring.data.repository.invocations

# ─── ENV ─────────────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/env
curl http://localhost:8080/actuator/env/server.port
curl http://localhost:8080/actuator/env/spring.application.name
curl http://localhost:8080/actuator/env/JAVA_HOME

# ─── BEANS ───────────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/beans

# ─── CONDITIONS ──────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/conditions

# ─── CONFIG PROPS ────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/configprops
curl http://localhost:8080/actuator/configprops/spring.datasource

# ─── MAPPINGS ────────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/mappings

# ─── LOGGERS ─────────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/loggers
curl http://localhost:8080/actuator/loggers/root
curl http://localhost:8080/actuator/loggers/org.springframework
curl http://localhost:8080/actuator/loggers/org.springframework.web
curl http://localhost:8080/actuator/loggers/org.hibernate

# Change log level (POST)
curl -X POST http://localhost:8080/actuator/loggers/root \
  -H "Content-Type: application/json" \
  -d '{"configuredLevel": "DEBUG"}'

curl -X POST http://localhost:8080/actuator/loggers/org.springframework \
  -H "Content-Type: application/json" \
  -d '{"configuredLevel": "TRACE"}'

# Reset log level
curl -X POST http://localhost:8080/actuator/loggers/root \
  -H "Content-Type: application/json" \
  -d '{"configuredLevel": null}'

# ─── THREAD DUMP ─────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/threaddump
curl http://localhost:8080/actuator/threaddump -H "Accept: text/plain"

# ─── HEAP DUMP ───────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/heapdump --output heapdump.hprof

# ─── SCHEDULED TASKS ─────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/scheduledtasks

# ─── CACHES ──────────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/caches
curl http://localhost:8080/actuator/caches/myCache

# Evict a specific cache
curl -X DELETE http://localhost:8080/actuator/caches/myCache

# Evict all caches
curl -X DELETE http://localhost:8080/actuator/caches

# ─── SESSIONS (Spring Session) ───────────────────────────────────────────────
curl "http://localhost:8080/actuator/sessions?username=myuser"
curl -X DELETE http://localhost:8080/actuator/sessions/SESSION_ID

# ─── SHUTDOWN (must be explicitly enabled) ───────────────────────────────────
curl -X POST http://localhost:8080/actuator/shutdown

# ─── FLYWAY ──────────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/flyway

# ─── LIQUIBASE ───────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/liquibase

# ─── PROMETHEUS (requires micrometer-registry-prometheus) ────────────────────
curl http://localhost:8080/actuator/prometheus

# ─── HTTP TRACE / EXCHANGES ──────────────────────────────────────────────────
# Spring Boot 2.x
curl http://localhost:8080/actuator/httptrace
# Spring Boot 3.x
curl http://localhost:8080/actuator/httpexchanges

# ─── STARTUP ─────────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator/startup

# ─── WITH AUTHENTICATION (if Spring Security is configured) ──────────────────
curl http://localhost:8080/actuator/health \
  -u admin:password

curl http://localhost:8080/actuator/env \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"

# ─── PRETTY PRINT ────────────────────────────────────────────────────────────
curl http://localhost:8080/actuator | python3 -m json.tool
curl http://localhost:8080/actuator/health | jq .
```
