# edu-intro-java

# Instruktioner

```bash
cd ~
cd ws
cd edu-intro-java #Återvänd till projektet
mkdir ./app/src/main/resources/static
touch ./app/src/main/resources/static/index.html
touch ./app/src/main/resources/static/index.css
touch ./app/src/main/resources/static/index.js
vi ./app/build.gradle
vi ./app/src/main/java/se/iths/App.java
vi ./app/src/test/java/se/iths/AppTest.java
vi ./app/src/main/resources/static/index.html
gradle bootRun
curl localhost:8080
```

## build.gradle

> Lägg till plugin för spring boot.
> id 'org.springframework.boot' version '2.6.2'

> Lägg till en plugin som håller reda på spring boot beroenden
> id 'io.spring.dependency-management' version '1.0.12.RELEASE'

> Ta bort application pluginnen och dess konfiguration

> Lägg till minimi dependency för spring boot
> implementation 'org.springframework.boot:spring-boot-starter-web:'

> Kolla gärna vilken version som är den senaste


```groovy
plugins {
    id 'java'
    id 'org.springframework.boot' version '2.6.2'
    id 'io.spring.dependency-management' version '1.0.12.RELEASE'
}

repositories {
     mavenCentral()
}

dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.8.1'
    
    implementation 'org.springframework.boot:spring-boot-starter-web:'
}

tasks.named('test') {
  useJUnitPlatform()
  testLogging.showStandardStreams = true
}
```

## App.java

> Märk upp App som en @SpringBootApplication

> Ändra så att applikationen startas som en spring boot applikation.

```java
package se.iths;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class App {

    public static void main(String[] args) {
        SpringApplication.run(App.class);
    }

}
```

## AppTest.java

> Ta bort asserten, men behåll testet ett tag till.
> 
```java
package se.iths;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class AppTest {
    @Test void appHasAGreeting() {

    }
}
```

## index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
```
