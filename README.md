# Gradle Cyclic Dependency Traverse Bug

When recursively traversing the transitive dependencies of a
`ResolvedConfiguration`, Gradle is unable to identify circular dependencies.
This causes Gradle to recurse until overflowing the stack space.

This defect is quite easy to reproduce. Steps shown below.

The upstream issue can be found [here](https://github.com/gradle/gradle/issues/22850).

## Steps to Reproduce

```
$ ./gradlew project-1-2-1:die
> Task :project-1-2-1:die FAILED

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':project-1-2-1:die'.
> java.lang.StackOverflowError (no error message)

* Try:
> Run with --stacktrace option to get the stack trace.
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 428ms
1 actionable task: 1 executed
```

