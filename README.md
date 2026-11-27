# HtBuilder – Kotlin Builder Code Generator

**HtBuilder** is a Kotlin code generation library that automatically generates Builder, Setter, and Getter methods using annotations and [Kotlin Symbol Processing (KSP)](https://github.com/google/ksp).

HtBuilder helps reduce boilerplate code and provides a clean, readable, and fluent API for Kotlin projects, including Android applications.

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
- Selective code generation through individual annotations.
- Full code generation with a single `@Data` annotation.

## Supported Annotations

HtBuilder provides four annotations:

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

The generated Setter methods can be used directly inside Kotlin's `apply {}` scope function.

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

## Using Setter and Getter with apply

HtBuilder supports using generated methods inside Kotlin scope functions.

This allows you to initialize and modify objects in a clean and readable way.

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

**Example:**

```kotlin
val request = RequestData().apply {
    setId(52)
    setAction("URL")
    setPayload(data)
}

val requestId = request.getId()
val requestAction = request.getAction()
```

## Installation

### 1. Add the KSP Plugin

Add the KSP plugin to your module-level `build.gradle.kts`:

```kotlin
plugins {
    id("com.google.devtools.ksp")
}
```

### 2. Add HtBuilder Dependencies

Add the following dependencies to your module-level `build.gradle.kts`:

```kotlin
dependencies {
    implementation("io.github.taros84:htdata-annotations:1.0.10")
    ksp("io.github.taros84:htdata-processor:1.0.10")
}
```

### 3. Maven Dependency

For Maven projects, add the annotations dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>io.github.taros84</groupId>
    <artifactId>htdata-annotations</artifactId>
    <version>1.0.10</version>
</dependency>
```

**Note:** The KSP processor must also be configured in your build system to generate code.

## Requirements

- Kotlin
- Kotlin Symbol Processing (KSP)
- Gradle
- Android Studio or IntelliJ IDEA

## Published Artifacts

| Artifact | Version |
|---|---|
| `htdata-annotations` | `1.0.10` |
| `htdata-processor` | `1.0.10` |

**Maven Group:** `io.github.taros84`

## License

See the [LICENSE](LICENSE) file for license information.
