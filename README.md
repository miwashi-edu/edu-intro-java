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
```

# gradle init

```bash
Select type of project to generate:
  1: basic
  2: application
  3: library
  4: Gradle plugin
Enter selection (default: basic) [1..4] 2
```


```bash
Select implementation language:
  1: C++
  2: Groovy
  3: Java
  4: Kotlin
  5: Scala
  6: Swift
Enter selection (default: Java) [1..6] 3
```

```bash
Split functionality across multiple subprojects?:
  1: no - only one application project
  2: yes - application and library projects
Enter selection (default: no - only one application project) [1..2] 1
```

```bash
Select build script DSL:
  1: Groovy
  2: Kotlin
Enter selection (default: Groovy) [1..2] 1
```

```bash
Generate build using new APIs and behavior (some features may change in the next minor release)? (default: no) [yes, no] [enter]
````

```bash
Select test framework:
  1: JUnit 4
  2: TestNG
  3: Spock
  4: JUnit Jupiter
Enter selection (default: JUnit Jupiter) [1..4] 4
```

```bash
Project name (default: edu-intro-java): [enter]
```

```bash
Source package (default: edu.intro.java): se.iths
```

## För hand

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
