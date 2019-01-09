This is a demonstration of [Gradle Issue 1812](https://github.com/gradle/gradle/issues/1812). It consists of three artifacts:

- `demo-artifact` is a Maven artifact with two direct dependencies,
- `test-maven` is a Maven artifact that depends on `demo-artifact`,
- `test-gradle` is a Gradle artifact that depends on `demo-artifact`.

The script `run` will

- compile `demo-artifact` and install it to the local Maven repository,
- invoke the `dependency:copy-dependencies` goal on `test-maven`,
- invoke the `copyDeps` task on `test-gradle`.

The expected behavior would be that both `test-maven/target/dependency` and `test-gradle/deps` will contain the same dependencies after running the script, and in particular that `jakarta.annotation-api-1.3.3.jar` will be one of those dependencies, and *not* `jakarta-annotation-api-1.3.4.jar`.

The actual behavior is that the Gradle script downloads `jakarta-annotation-api-1.3.4.jar` instead of `jakarta-annotation-api-1.3.3.jar`.

To reproduce, just download the demo and invoke

```
  ./run
```
