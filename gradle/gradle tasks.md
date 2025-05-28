Instead of remembering complex command sequences, create tasks

```gradle
task deployToStaging {
    doLast {
        // Custom deployment logic
        exec { commandLine 'docker', 'build', '-t', 'myapp', '.' }
        exec { commandLine 'kubectl', 'apply', '-f', 'staging.yaml' }
    }
}
```

Now `./gradlew deployToStaging` handles entire deployment pipeline.
