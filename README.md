# edu-intro-java

# Instruktioner

```bash
cd ~
cd ws
rm -rf edu-intro-java #Försiktig med denna
mkdir edu-intro-java
cd edu-intro-java
gradle init #svara på frågor
gradle check
gradle run
vi ./app/build.gradle
vi ./app/src/main/java/se/iths/App.java
vi ./app/src/test/java/se/iths/AppTest.java
```

## build.gradle

```groovy
plugins {
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

```java
package se.iths;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class AppTest {
    @Test void appHasAGreeting() {

    }
}
```
