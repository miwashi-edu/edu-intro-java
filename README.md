# edu-intro-java

> Omvandlar en java applikation till en Spring Boot applikation

# Instruktioner

```bash
cd ~
cd ws
cd edu-intro-java
mkdir ./app/src/main/resources/static
touch ./app/src/main/resources/static/{index.html,index.js,index.css}
curl -L https://gist.github.com/miwashiab/e393185947f8b29d064746d1633c5a4d/raw/build.gradle -o ./app/build.gradle
curl -L https://gist.github.com/miwashiab/44bb4bc1d82f0952ffbf6c55fbd63ec8/raw/index.html -o ./app/src/main/resources/static/index.html
curl -L https://gist.github.com/miwashiab/018e7eb1c7b9556e4c2ac5076a6126a0/raw/App.java -o ./app/src/main/java/se/iths/App.java
curl -L https://gist.github.com/miwashiab/0ca40c177e62925e8dbb973229a4299d/raw/AppTest.java -o ./app/src/test/java/se/iths/AppTest.java
git add .
git commit -m "Changed to Spring Boot Application"
gradle bootRun
```

```bash
curl http://localhost:8080
```

## build.gradle

```bash
vi ./app/build.gradle
```

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

## App.java

```bash
vi ./app/src/test/java/se/iths/App.java
```

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

## AppTest.java

```bash
vi ./app/src/test/java/se/iths/AppTest.java
```

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

## index.html

```bash
vi ./app/src/main/resources/static/index.html
```

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

## build.gradle

```groovy
plugins {
    id 'application'
}

repositories {
    mavenCentral()
}

dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.8.2'
}

application {
    mainClass = 'se.iths.App'
}

tasks.named('test') {
    useJUnitPlatform()
    testLogging.showStandardStreams = true
}
```
