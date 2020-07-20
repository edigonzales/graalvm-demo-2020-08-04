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
- JNIReflectionClasses
- Config-Files
- Tracing Agent: https://www.graalvm.org/docs/reference-manual/native-image/#tracing-agent




- startup mit java
- agent / feature
- json config files 
- kompilieren (docker multi stage)
- start up native
- fehler provozieren "not supported feature"
- ci/cd pipeline (anderes repo)