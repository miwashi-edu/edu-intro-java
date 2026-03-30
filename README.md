# edu-intro-java

## Prepare

```bash
cd ~
cd ws
cd intro-java
git add .
git commit -m "level-3"
```


## Instructions

```bash
cd ~
cd ws
cd intro-java
```

### ./src/main/java/net/miwashi/controllers/AuthController.java

```bash
cat > ./src/main/java/net/miwashi/controllers/AuthController.java << 'EOF'

EOF
```

### New Dependencies

> We add TRACE logging.
> We add ACCESS logging.
> We add JASYPT.
> We add Lombook.
> We add Hibernate Validator

```groovy
dependencies {
  compileOnly 'org.projectlombok:lombok'
  annotationProcessor 'org.projectlombok:lombok'
  implementation 'com.github.ulisesbocchio:jasypt-spring-boot-starter:3.0.5'
  implementation 'org.springframework.boot:spring-boot-starter-validation'
}
```

### ./app/src/main/resources/application.properties 

```bash
jasypt.encryptor.password=${JASYPT_ENCRYPTOR_PASSWORD:password}
logging.level.net.miwashi.controllers=TRACE
```

### ./app/src/main/resources/application-dev.properties 

```bash
jwt.key=ENC(7uB0v44fN2y6W1O8+hVn7g==)
```
### ./app/src/main/resources/application-stage.properties 

```bash
jwt.key=ENC(7uB0v44fN2y6W1O8+hVn7g==)
```


### ./app/src/main/resources/application-prod.properties 

```bash
jwt.key=ENC(7uB0v44fN2y6W1O8+hVn7g==)
```

## Repeat

```bash
git reset --hard
git clean -df
```

## Test it

```bash
```
