# edu-intro-java

> I detta steg lägger vi inte till mycket. Vi bara förbereder att vi har två mijöer, utveckling och produktion.

# Instruktioner

```bash
cd ~
cd ws
cd edu-intro-java
touch ./app/src/main/resources/{application.properties,application-dev.properties,application-prod.properties]
echo 'spring.profiles.active=${ENV:dev}\nserver.port=${PORT:8081}' > ./app/src/main/resources/application.properties
echo "spring.devtools.restart.enabled=true" > ./app/src/main/resources/application-dev.properties
echo "spring.devtools.restart.enabled=false" > ./app/src/main/resources/application-prod.properties
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
