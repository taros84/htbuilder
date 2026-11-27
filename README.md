# HtBuilder – Kotlin Builder Generator

**HtBuilder** is a Kotlin Builder code generation library for Android Studio and Kotlin projects.

It allows you to automatically generate Builder patterns for Kotlin classes using annotations and KSP (Kotlin Symbol Processing).

## Features

- Automatic Builder code generation.
- Supports Kotlin `data class` and regular classes.
- Supports nullable and non-nullable properties.
- Supports default property values.
- Uses KSP for compile-time code generation.
- Simple annotation-based implementation.

## Installation

### 1. Add the KSP plugin

Add the KSP plugin to your module-level `build.gradle.kts`:

```kotlin
plugins {
    id("com.google.devtools.ksp")
}
```

### 2. Add HtBuilder dependencies

Add the following dependencies to your module-level `build.gradle.kts`:

```kotlin
dependencies {
    implementation("io.github.taros84:htdata-annotations:1.0.10")
    ksp("io.github.taros84:htdata-processor:1.0.10")
}
```
### 3. Maven (pom.xml):

```xml
<dependency>
    <groupId>io.github.taros84</groupId>
    <artifactId>htdata-annotations</artifactId>
    <version>1.0.10</version>
</dependency>
```

## Usage

### 1. Import the Builder,Data,Setter,Getter annotation

```kotlin
import io.github.taros84.Data
or
import io.github.taros84.Builder
or
import io.github.taros84.Setter
or
import io.github.taros84.Getter
```

### 2. Annotate your class

Add the `@Data` or `@Builder` or `@Setter` or `@Getter` annotation to your Kotlin class.
Add `@Data` full object import 

**Example:**

```kotlin
@Builder
data class RequestData(
    var id: Int = 0,
    var action: String? = null,
    var payload: Any? = null
) {
    companion object
}
```

> **Note:** Add `companion object` to the class to enable the generated Builder access through `RequestData.builder()`.

### 3. Create an object using Builder

After KSP generates the Builder code, you can create objects using the following syntax:

```kotlin
val request = RequestData.builder()
    .id(52)
    .action("URL")
    .payload(object)
    .build()
```

## Example

Instead of manually creating objects using constructors:

```kotlin
val request = RequestData(
    id = 52,
    action = "URL",
    payload = object
)
```

You can use the generated Builder pattern:

```kotlin
val request = RequestData.builder()
    .id(52)
    .action("URL")
    .payload(object)
    .build()
```

## Requirements

- Kotlin
- Android Studio or IntelliJ IDEA
- Kotlin Symbol Processing (KSP)

## License

See the repository's LICENSE file for license information.
