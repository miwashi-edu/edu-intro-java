# edu-intro-java

# Create Workspace

```bash
cd ~
mkdir ws
```

# Prepare

```bash
cd ~
cd ws
mkdir intro-java
cd intro-java
curl -o .gitignore https://raw.githubusercontent.com/github/gitignore/main/Java.gitignore
echo "# Intro Java" > README.md
git init
git add .
git commit -m "Initial Commit"
```


# Instructions

```bash
cd ~
cd ws
cd intro-java
mkdir -p ./app/src/main/{java/net/miwashi,resources}
mkdir -p ./app/src/test/{java/net/miwashi,resources}
touch ./app/src/main/java/net/miwashi/App.java
touch ./app/src/test/java/net/miwashi/AppTest.java
touch ./app/build.gradle
touch settings.gradle
touch gradle.properties
```

## App.java

```java
cat > ./app/src/main/java/net/miwashi/App.java << 'EOF'
package net.miwashi;

public class App {

    public static void main(String[] args){
        System.out.println("Hello World");
    }
}
EOF
```


## AppTest.java

```java
cat > ./app/src/test/java/net/miwashi/AppTest.java << 'EOF'
package net.miwashi;

import org.junit.jupiter.api.Test;

public class AppTest {

    @Test
    public void shouldTestSomething() throws Exception {
        System.out.println("Testing World");
    }
}
EOF
```

## ./app/build.gradle

```bash
cat > ./app/build.gradle << 'EOF'
plugins {
    id 'application'
}

repositories {
    mavenCentral()
}

dependencies {
    testImplementation("org.junit.jupiter:junit-jupiter-api:5.12.1")
    testRuntimeOnly("org.junit.jupiter:junit-jupiter-engine:5.12.1")
    testRuntimeOnly("org.junit.platform:junit-platform-launcher:1.12.1")
}

java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(21)
    }
}

application {
    mainClass = 'net.miwashi.App'
}

tasks.named('test') {
    useJUnitPlatform()
    testLogging.showStandardStreams = true
}
EOF
```

## settings.gradle

```bash
cat > settings.gradle << 'EOF'
plugins {
    id 'org.gradle.toolchains.foojay-resolver-convention' version '0.10.0'
}

rootProject.name = 'intro-java'
include('app')
EOF
```
## gradle.properties

```bash
cat > gradle.properties << 'EOF'
org.gradle.configuration-cache=true
EOF
```

## Test it

```bash
gradle run
gradle test
gradle check
```

## Repeat it

```bash
git reset --hard
git clean -df
```


