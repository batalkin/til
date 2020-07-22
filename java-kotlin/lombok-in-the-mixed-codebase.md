# Lombok in the mixed codebase (Java+Kotlin)

Lombok does not work well in codebase with Kotlin and Java mixed:

```java
import lombok.Builder;

/**
 * Some Java class with any Lombok annotation.
 * Here I took @Builder but it does not matter
 */
@Builder
public class SomePojo {
    private final String someField;
}

```

Using this class from Kotlin code looks like the following:

```kotlin
class SomeKotlinClass {
    fun someMethod() {
        SomePojo.builder()
                .build()
    }
}
```

This lead to a sad compilation error

```
❗Error:(5, 18) Kotlin: Unresolved reference: builder
```

To compile a mixed codebase Kotlin compiler should be invoked before Java compiler. Kotlin compiler still compiles java classes to check that Kotlin classes are valid but **it does not run annotation processors**. So Lombok code is not yet generated when Kotlin classes are compiled.  

There are some options to go around it and run delombok maven plugin to generate java files without annotation before compilation. This option is a bit messy since original annotated classes need to be placed in some odd location like `src/main/lombok`.

What I did when faced this issue? Rewrote my class from Kotlin to Java.