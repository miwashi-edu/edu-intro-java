# edu-intro-java

# Instruktioner

```bash
touch ./app/src/main/resources/application.properties
touch ./app/src/main/resources/application-dev.properties
touch ./app/src/main/resources/application-prod.properties
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

## ./app/src/main/resources/application.properties

```properties
spring.profiles.active=${ENV:dev}

#Ta bort denna när vi är klara
# detta är bara för att vi ska se
# att vår våra inställningar fungerar
server.port=8081
jdbc.url=Detta kommer att bli en connection string!
```

## ./app/src/main/resources/application-dev.properties

```properties
spring.devtools.restart.enabled=true

#Ta bort denna när vi är klara
# detta är bara för att vi ska se
# att vår våra inställningar fungerar
server.port=8082
```

## ./app/src/main/resources/application-prod.properties

```properties
spring.devtools.restart.enabled=false

#Ta bort denna när vi är klara
# detta är bara för att vi ska se
# att vår våra inställningar fungerar
server.port=8083
```
