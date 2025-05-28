gradle is pip and [[docker]] for production java

- **pip + setuptools + make + shell scripts** all rolled into one
- It's a **build system** that handles dependencies AND orchestrates your entire build process
## **Build automation**

While traditional Java development might have you manually downloading JAR files, setting classpaths, and running javac commands, Gradle automates all of this tedious work.

**Before Gradle (Traditional Method):**

```
1. Download Spring JAR → Download Jackson JAR → Download MySQL connector
2. Set CLASSPATH environment variable with 20+ JAR paths
3. javac -cp "long/path/to/jars/*" src/*.java
4. java -cp "same/long/path" MainClass
5. Repeat this nightmare for every dependency update
```

**With Gradle:**

```gradle
dependencies {
    implementation 'org.springframework:spring-web:5.3.21'
    implementation 'com.fasterxml.jackson.core:jackson-core:2.13.3'
    implementation 'mysql:mysql-connector-java:8.0.29'
}
```

Run `./gradlew build`

---
- Gradle automatically resolves transitive dependencies. If Spring needs 15 other libraries, Gradle fetches them all.
- no version conflicts
---
[[gradle tasks]] works similar to a [[dockerfile]]
