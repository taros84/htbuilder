# HtBuilder – Kotlin Builder Code Generator

**HtBuilder** is a Kotlin code generation library that automatically generates Builder, Setter, and Getter methods using annotations and [Kotlin Symbol Processing (KSP)](https://github.com/google/ksp).

HtBuilder reduces boilerplate code and provides a clean, readable, and type-safe API for Kotlin projects, including Android applications.

## Features

- Automatic Builder pattern generation.
- Automatic Setter method generation.
- Automatic Getter method generation.
- Supports Kotlin `data class` and regular classes.
- Supports nullable and non-nullable properties.
- Supports properties with default values.
- Annotation-based code generation.
- Compile-time processing using KSP.
- Type-safe generated Kotlin code.
- Supports Kotlin `apply {}` scope function.
- Selective code generation using individual annotations.
- Full code generation using a single `@Data` annotation.

## Supported Annotations

HtBuilder provides four annotations for controlling code generation.

| Annotation | Builder | Setter | Getter |
|---|:---:|:---:|:---:|
| `@Data` | ✓ | ✓ | ✓ |
| `@Builder` | ✓ | – | – |
| `@Setter` | – | ✓ | – |
| `@Getter` | – | – | ✓ |

### 1. @Data – Full Code Generation

The `@Data` annotation enables all available code generation features:

- Builder
- Setter
- Getter

**Class definition:**

```kotlin
@Data
data class User(
    var id: Int = 0,
    var name: String? = null
) {
    companion object
}
```

**Usage:**

```kotlin
// Builder
val user = User.builder()
    .id(10)
    .name("Halil")
    .build()

// Setter
user.setId(20)
user.setName("Ahmet")

// Getter
val id = user.getId()
val name = user.getName()
```

### 2. @Builder – Builder Only

The `@Builder` annotation generates only Builder functionality.

**Class definition:**

```kotlin
@Builder
data class Product(
    var id: Int = 0,
    var name: String? = null
) {
    companion object
}
```

**Usage:**

```kotlin
val product = Product.builder()
    .id(10)
    .name("Laptop")
    .build()
```

### 3. @Setter – Setter Only

The `@Setter` annotation generates only Setter methods.

**Class definition:**

```kotlin
@Setter
data class Account(
    var username: String = "",
    var balance: Double = 0.0
)
```

**Usage with apply:**

```kotlin
val account = Account().apply {
    setUsername("Halil")
    setBalance(1500.0)
}
```

**Usage without apply:**

```kotlin
val account = Account()

account.setUsername("Halil")
account.setBalance(1500.0)
```

### 4. @Getter – Getter Only

The `@Getter` annotation generates only Getter methods.

**Class definition:**

```kotlin
@Getter
data class Customer(
    var id: Int = 0,
    var name: String = ""
)
```

**Usage:**

```kotlin
val customer = Customer(
    id = 1,
    name = "Halil"
)

val customerId = customer.getId()
val customerName = customer.getName()
```

## Using Setter and Getter with Kotlin apply

HtBuilder supports using generated methods inside Kotlin scope functions such as `apply {}`.

This allows objects to be initialized and modified with a clean and readable syntax.

**Class definition:**

```kotlin
@Data
data class RequestData(
    var id: Int = 0,
    var action: String? = null,
    var payload: Any? = null
) {
    companion object
}
```

**Usage:**

```kotlin
val request = RequestData().apply {
    setId(52)
    setAction("URL")
    setPayload(data)
}

// Getter
val requestId = request.getId()
val requestAction = request.getAction()
val requestPayload = request.getPayload()
```

## Builder Example

Instead of manually creating objects using constructors:

```kotlin
val request = RequestData(
    id = 52,
    action = "URL",
    payload = data
)
```

You can use the generated Builder pattern:

```kotlin
val request = RequestData.builder()
    .id(52)
    .action("URL")
    .payload(data)
    .build()
```

The Builder pattern provides a fluent API for creating objects and makes object initialization easier to read and maintain.

## Requirements

HtBuilder uses the following build tool versions:

| Tool | Version |
|---|---|
| Gradle | 9.6.0 |
| Kotlin | 2.3.20 |
| Kotlin Symbol Processing (KSP) | 2.3.12 |

Additional requirements:

- JDK compatible with Gradle 9.6.0
- Android Studio or IntelliJ IDEA
- Kotlin-based Gradle project

## Installation

### 1. Configure Kotlin and KSP Plugins

Add the following plugins to your root-level `build.gradle.kts`:

```kotlin
plugins {
    kotlin("jvm") version "2.3.20" apply false
    id("com.google.devtools.ksp") version "2.3.12" apply false
}
```

### 2. Apply Plugins to Your Module

For Kotlin JVM projects, add the following to your module-level `build.gradle.kts`:

```kotlin
plugins {
    kotlin("jvm")
    id("com.google.devtools.ksp")
}
```

For Android projects, apply the appropriate Android application or library plugin together with the compatible Kotlin Android and KSP plugins.

### 3. Add HtBuilder Dependencies

Add the following dependencies to your module-level `build.gradle.kts`:

```kotlin
dependencies {
    implementation("io.github.taros84:htdata-annotations:1.0.10")
    ksp("io.github.taros84:htdata-processor:1.0.10")
}
```

### 4. Configure Maven Repository

Make sure Maven Central is included in your project repositories:

```kotlin
repositories {
    mavenCentral()
}
```

### 5. Generate Code

Build your project to trigger KSP code generation:

```bash
./gradlew clean build
```

On Windows:

```powershell
.\gradlew clean build
```

After a successful build, generated Kotlin source files will be available in the KSP generated sources directory.

## Maven Installation

For Maven projects, add the annotations dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>io.github.taros84</groupId>
    <artifactId>htdata-annotations</artifactId>
    <version>1.0.10</version>
</dependency>
```

**Note:** HtBuilder uses KSP for compile-time code generation. The KSP processor must also be integrated into the build process. Adding the annotations dependency alone does not execute KSP.

## Published Artifacts

HtBuilder is published under the following Maven coordinates:

| Artifact | Version |
|---|---|
| `htdata-annotations` | `1.0.10` |
| `htdata-processor` | `1.0.10` |

**Group ID:** `io.github.taros84`

**Repository:** Maven Central

## License

See the [LICENSE](LICENSE) file for license information.
