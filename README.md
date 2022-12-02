# edu-intro-java

# Instruktioner

```bash
cd ~
cd ws
rm -rf edu-intro-java #Försiktig med denna
mkdir edu-intro-java
cd edu-intro-java
mkdir -p ./app/src/main/{java/se/iths,resources}
mkdir -p ./app/src/test/{java/se/iths,resources}
touch ./app/src/main/java/se/iths/App.java
touch ./app/src/test/java/se/iths/AppTest.java
touch ./app/build.gradle
echo "# edu-intro-java" > README.md
echo "rootProject.name = 'edu-intro-java'\ninclude('app')" > settings.gradle
curl -L https://gist.githubusercontent.com/miwashiab/987826fc0f2df3cd686a755f38a1c504/raw/build.gradle -o ./app/build.gradle
echo ".idea\n.gradle\nbuild\n*.log" > .gitignore
git init
git add .
git commit -m "Initial commit"
```

## App.java

```java
package se.iths;

public class App {

    public static void main(String[] args){
        System.out.println("Hello World");
    }
}
```


## AppTest.java

```java
package se.iths;

import org.junit.jupiter.api.Test;

public class AppTest {

    @Test
    public void shouldTestSomething() throws Exception {
        System.out.println("Testing World");
    }
}
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
