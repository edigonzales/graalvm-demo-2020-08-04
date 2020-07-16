# graalvm-demo-2020-08-04

## ili2gpkg web service

### Java
```
mvn clean install
```

```
java -jar target/ili2gpkg-web-service-0.0.1-SNAPSHOT.jar
```

```
http://localhost:8080/
```

XTF / ITF hochladen. Log messages in Terminal zeigen.

### GraalVM
Wegen SQLite-Abhängigkeit braucht es eine zusätzliche Klasse (`JNIReflectionClasses`). Ich bin mir nicht sicher, ob es eine zusätzliche Komplexität wegen der Art wie diese SQLite-Bibliothek in Java funktioniert oder aber bloss um die programmatische Umsetzung von dem ist, was man für GraalVM sonst in Config-Files hat.

- agent...




- startup mit java
- agent / feature
- json config files 
- kompilieren (docker multi stage)
- start up native
- fehler provozieren "not supported feature"
- ci/cd pipeline (anderes repo)