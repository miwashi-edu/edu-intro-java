# edu-intro-java

> Omvandlar en java applikation till en Spring Boot applikation


# Prepare

```bash
cd ~
cd ws
cd intro-java
git add .
git commit -m "Level-0"
```

# Instruktioner

```bash
cd ~
cd ws
cd intro-java
mkdir ./app/src/main/resources/static
touch ./app/src/main/resources/static/{index.html,index.js,index.css}
touch ./app/src/main/resources/application.properties
```

## build.gradle

```bash
cat > ./app/build.gradle << 'EOF'
plugins {
	id 'java'
	id 'org.springframework.boot' version '4.0.4'
	id 'io.spring.dependency-management' version '1.1.7'
}

group = 'net.miwashi'
version = '0.0.1-SNAPSHOT'

java {
	toolchain {
		languageVersion = JavaLanguageVersion.of(21)
	}
}

repositories {
	mavenCentral()
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
}

tasks.named('test') {
	useJUnitPlatform()
    testLogging.showStandardStreams = true
}
EOF
```

## App.java

```bash
cat > ./app/src/test/java/net/miwashi/App.java << 'EOF'
package net.miwashi;

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
cat > ./app/src/test/java/net/miwashi/AppTest.java << 'EOF'
package net.miwashi;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class AppTests {
	@Test
	void contextLoads() {
	}
}
EOF
```

## index.html

```bash
cat > ./app/src/main/resources/static/index.html << 'EOF'
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
EOF
```

## Test it

```bash
cd ~
cd ws
cd intro-java
gradle bootRun
curl http://localhost:8080
```

## Repeat

```bash
cd ~
cd ws
cd intro-java
git reset --hard
git clear -df
```
