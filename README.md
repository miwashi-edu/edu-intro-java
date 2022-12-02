# edu-intro-java

> I detta steg driftsätter vi vår applikation till Heroku.

## Windows
> I Windows, starta Powershell som Admin.

```bash
choco install heroku-cli
```

## Mac

> I mac 

```bash
brew tap heroku/brew && brew install heroku
```

# Instruktioner

```bash
cd ~
cd ws
cd edu-intro-java
echo 'web: java $JAVA_OPTS -jar ./app/build/libs/app.jar' > Procfile
echo "task copyToLib(type: Copy) {\n\tinto "$buildDir/libs"\n\tfrom(configurations.implementation)\n}\n\nstage.dependsOn(copyToLib)" >> ./app/build.gradle
git add .
git commit -m "Added Procfile"
heroku login
heroku create [namn_på_applikation]
heroku config:set ENV=prod
git push heroku main # OM er gren heter master, git push heroku master:main
heroku open
```
