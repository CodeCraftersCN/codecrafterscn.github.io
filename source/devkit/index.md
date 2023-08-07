---
title: devkit
date: 2023-08-07 16:24:52
---

# JDevKit

JDevKit is a Java Development Kit that offers a set of convenient tools for writing code efficiently.

## Modules

> For more information, please visit the README file of each module.

### `devkit-core` <span style="font-size: 12px;">_[Learn more](/devkit/devkit-core)_</span>

The core module for `JDevKit`, by now, this module contains the commonly used classes of the whole `dev-kit`.

### `devkit-utils` <span style="font-size: 12px;">_[Learn more](/devkit/guid)_</span>

A collection of common utility classes to simplify Java development. It includes tools for Base64 encoding/decoding of
strings, reducing if-else code blocks using Lambda expressions, converting between maps and arbitrary objects,
high-precision chained mathematical calculations, and string hashing or message digest calculations.

### `guid` <span style="font-size: 12px;">_[Learn more](/devkit/devkit-utils)_</span>

A module for generating globally unique IDs. It includes a facade interface and an implementation of GUID generation
using the Snowflake algorithm. More globally unique ID generation modes will be added in the future.

### `webcal` <span style="font-size: 12px;">_[Learn more](/devkit/webcal)_</span>

The module `webcal` is a Java library that facilitates the generation and resolution of iCalendar content for web-based
calendar applications. It provides a flexible and easy-to-use API for creating web calendars with customizable settings
and events.

With the `webcal` module, developers can easily integrate calendar functionality into web applications, enabling users
to view, add, and manage events in a structured and standardized format. It is designed to simplify calendar-related
tasks and enhance the overall user experience when dealing with calendar data on the web.

Please note that the `webcal` module adheres to the iCalendar standard specified in RFC 5545, ensuring compatibility
with other calendar applications that support this format.

### `simple-jwt-facade` <span style="font-size: 12px;">_[Learn more](/devkit/simple-jwt-facade)_</span>

A facade for Simple JWT (JSON Web Token) implementations in Java. This module provides a unified interface to work with
JWTs regardless of the underlying implementation.

### `simple-jwt-authzero` <span style="font-size: 12px;">_[Learn more](/devkit/simple-jwt-authzero)_</span>

A Simple JWT implementation using the com.auth0:java-jwt library.

### `simple-jwt-spring-boot-starter` <span style="font-size: 12px;">_[Learn more](/devkit/simple-jwt-spring-boot-starter)_</span>

A Spring Boot auto-configuration wrapper for the simple-jwt module, making it easier to integrate JWT functionality into
Spring Boot applications.

## Installation and Usage

If you are using `maven`, please paste the following codes to `pom.xml` in your project.

```xml 
<dependency>
	<groupId>cn.org.codecrafters</groupId>
    <artifactId>${artifactId}</artifactId>
    <version>${version}</version>
</dependency>
```

If you are using `gradle`, please paste the following codes to `buile.gradle` in your project.

```groovy
implementation 'cn.org.codecrafters:$artifactId:$version'
```

## Contribution

Contributions are welcome! If you encounter any issues or want to contribute to the project, please feel free to 
**[raise an issue](https://github.com/CodeCraftersCN/jdevkit/issues/new)** or **[submit a pull request](https://github.com/CodeCraftersCN/jdevkit/compare)**.

## License

This project is licensed under the [Apache License 2.0](LICENSE).

## Contact

If you have any suggestions, ideas, don't hesitate contacting us via [GitHub Issues](https://github.com/CodeCraftersCN/jdevkit/issues/new)
or [Discord Community](https://discord.gg/NQK9tjcBB8).

If you face any bugs while using our library and you are able to fix any bugs in our library, we would be happy to
accept pull requests from you on [GitHub](https://github.com/CodeCraftersCN/jdevkit/compare).
