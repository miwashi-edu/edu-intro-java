# edu-intro-java

# Instruktioner

```bash
cd ~
cd ws
cd edu-intro-java
mkdir ./app/src/main/resources/static
touch ./app/src/main/resources/static/{index.html,index.js,index.css}
```

## ./app/build.gradle
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
    implementation 'org.springframework.boot:spring-boot-starter-web'
    
    testImplementation 'org.junit.jupiter:junit-jupiter:5.8.1'
}

tasks.named('test') {
    useJUnitPlatform()
    testLogging.showStandardStreams = true
}
```

## ./app/src/main/java/se/iths/App.java

```java
package se.iths;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class App {

  public static void main(String[] args) {
        SpringApplication.run(App.class, args);
  }
}
```

## ./app/src/test/java/se/iths/AppTest.java

```java
package se.iths;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class AppTest {
    @Test void appHasAGreeting() {
        App classUnderTest = new App();
    }
}
```

## ./app/src/main/resources/static/index.html

```html
<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="/index.css">
    </head>
    <body>
        <h1>Hello World</h1>
        <script src='/index.js'/>
    </body>
</html>
```

