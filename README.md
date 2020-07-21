# graalvm-demo-2020-08-04

## Native Image (ili2gpkg web service)

https://github.com/edigonzales/ili2gpkg-web-service

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
- Erstellen des native images mittels Docker multistage. MacOS einiges langsamer als Linux pur.

```
docker run --rm --name ili2gpkg-web-service -p8080:8080 sogis/ili2gpkg-web-service
```

- Startup time: 0.2s vs. 2.3s.
- Google Cloud Run
- Serverless
- ...

Fehler provozieren mit `ch.so.kataster-belasteter-standorte.oereb.xtf`. Siehe https://github.com/claeis/ili2db/issues/354

### CI/CD Pipeline
(c) https://blogs.oracle.com/developers/building-cross-platform-native-images-with-graalvm

- Beispiel-CI/CD-Pipeline mit Github Actions
- Linux, macOS und Windows Binaries
- https://github.com/edigonzales/ili2c-native/ Alles GUI-Zeugs in main-Klasse auskommentiert.
- https://github.com/edigonzales/ili2c-native/blob/master/.github/workflows/ili2c.yaml
- https://github.com/edigonzales/ili2c-native/actions/runs/165841716
- https://github.com/edigonzales/ili2c-native/releases/tag/v0.0.12

Wo Java angenehmer/einfacher ist: Native image für macOS nicht direkt lauffähig, da unbekannter Entwickler. Entweder freischalten oder bezahlen.

## Shared Library (ili2c)

https://github.com/edigonzales/ili2c-api
https://github.com/edigonzales/ili2c/blob/graal-native/GRAALVM.md

- Eine Methode von ili2c `getLastModelName` als Shared Library erstellen. In einem C++-Programm diese Libray verwenden.
- Annotation `@CEntryPoint`
- Methode muss statisch sein

Fatjar erstellen (Bequemlichkeit, ansonsten alles im Classpath auflisten):

```
./gradlew clean build shadowJar
native-image --no-server -cp build/libs/ili2c-api-all.jar --shared -H:Name=libili2c
```

- Config-Dateien werden aus einem ili2c-graal-ready-Build verwendet: https://github.com/edigonzales/ili2c/blob/graal-native/GRAALVM.md
- `libili2c.dylib`, `libili2c.h`, `libili2c_dynamic.h`, `graal_isolate.h`, `graal_isolate_dynamic.h`
- Super-Dummy-C++-Programm: `getlastmodelname.c`

```
cc -Wall -I. -L. -lili2c getlastmodelname.c -o getlastmodelname
```

```
./getlastmodelname ./SO_AGI_AV_GB_Administrative_Einteilungen_Publikation_20180822.ili
./getlastmodelname /Users/stefan/tmp/GraalVM/Nutzungsplanung_V1_1.ili
```

- Kann man damit was machen? Spätere Diskussion?
- Python-Bindings?