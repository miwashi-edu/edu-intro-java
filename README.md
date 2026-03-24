# edu-intro-java

> I detta steg lägger vi inte till mycket. Vi bara förbereder att vi har två mijöer, utveckling och produktion.

# Prepare

```bash
cd ~
cd ws
cd intro-java
git add .
git commit -m "Level-1"
```

# Instruktioner

```bash
cd ~
cd ws
cd intro-java
touch ./app/src/main/resources/{application.properties,application-dev.properties,application-prod.properties}
```

## ./app/src/main/resources/application.properties
```bash
cat > ./app/src/main/resources/application.properties << 'EOF'
spring.profiles.active=${ENV:prod}
server.port=${PORT:8080}
spring.devtools.restart.enabled=false
EOF
```

## ./app/src/main/resources/application-dev.properties
```bash
cat > ./app/src/main/resources/application.properties << 'EOF'
server.port=${PORT:8081}
spring.devtools.restart.enabled=true
EOF
```

## ./app/src/main/resources/application-stage.properties
```bash
cat > ./app/src/main/resources/application.properties << 'EOF'
server.port=${PORT:8082}
spring.devtools.restart.enabled=true
EOF
```

## ./app/build.gradle

> Lägg till beroende till spring-boot-devtools.

```groovy
plugins {
    id 'org.springframework.boot' version '2.6.4'
    id 'io.spring.dependency-management' version '1.0.11.RELEASE'
    id 'java'
}

repositories {
    mavenCentral()
}

dependencies {
    developmentOnly("org.springframework.boot:spring-boot-devtools")
    
    implementation 'org.springframework.boot:spring-boot-starter-web'
    
    testImplementation 'org.junit.jupiter:junit-jupiter:5.8.1'
}

tasks.named('test') {
    useJUnitPlatform()
    testLogging.showStandardStreams = true
}
```

## application.properties


```bash
vi ./app/src/main/resources/application.properties
```

```properties
spring.profiles.active=${ENV:dev}

#Ta bort denna när vi är klara
# detta är bara för att vi ska se
# att vår våra inställningar fungerar
server.port=8081
```

## application-dev.properties


```bash
vi ./app/src/main/resources/application-dev.properties
```

```properties
spring.devtools.restart.enabled=true

#Ta bort denna när vi är klara
# detta är bara för att vi ska se
# att vår våra inställningar fungerar
server.port=8082
```

## application-prod.properties

```bash
vi ./app/src/main/resources/application-prod.properties
```

```properties
spring.devtools.restart.enabled=false

#Ta bort denna när vi är klara
# detta är bara för att vi ska se
# att vår våra inställningar fungerar
server.port=8083
```
