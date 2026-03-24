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
cat > ./app/src/main/resources/application-dev.properties << 'EOF'
server.port=${PORT:8081}
spring.devtools.restart.enabled=true
EOF
```

## ./app/src/main/resources/application-stage.properties
```bash
cat > ./app/src/main/resources/application-stage.properties << 'EOF'
server.port=${PORT:8082}
spring.devtools.restart.enabled=true
EOF
```

## ./app/build.gradle

> Lägg till beroende till spring-boot-devtools.

```groovy
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
	implementation 'org.springframework.boot:spring-boot-starter-web'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	testRuntimeOnly 'org.junit.platform:junit-platform-launcher'
	developmentOnly("org.springframework.boot:spring-boot-devtools")
}

tasks.named('test') {
	useJUnitPlatform()
    testLogging.showStandardStreams = true
}

tasks.register("bootDev", BootRun) {
    group = "application"
    description = "Run app with dev profile"

    classpath = sourceSets.main.runtimeClasspath
    mainClass.set("se.miwashi.App")
    systemProperty "spring.profiles.active", "dev"
}


tasks.register("bootStage", BootRun) {
    group = "application"
    description = "Run app with dev profile"

    classpath = sourceSets.main.runtimeClasspath
    mainClass.set("se.miwashi.App")
    systemProperty "spring.profiles.active", "stage"
}
EOF
```

## Try it

### Prod

```bash
gradle bootRun
curl http://localhost:8080
```
