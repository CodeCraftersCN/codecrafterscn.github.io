# Module `simple-jwt-facade`

## Introduction

The `simple-jwt-facade` module is a lightweight and easy-to-use façade for working with JSON Web Tokens (JWT) in Java applications. It provides a simplified interface and utilities to handle the creation, validation, renewal, and processing of JWTs without the need for complex configurations or third-party dependencies.

## Prerequisites

This whole `JDevKit` is developed by **JDK 17**, which means you have to use JDK 17 for better experience.

## Installation

### If you are using `Maven`

It is quite simple to install this module by `Maven`. The only thing you need to do is find your `pom.xml` file in the project, then find the `<dependencies>` node in the `<project>` node, and add the following codes to `<dependencies>` node:

```xml
<dependency>
	<groupId>cn.org.codecrafters</groupId>
    <artifactId>simple-jwt-facade</artifactId>
    <version>${simple-jwt-facade.version}</version>
</dependency>
```

And run `mvn dependency:get` in your project root folder(i.e., if your `pom.xml` is located at `/path/to/your/project/pom.xml`, then your current work folder should be `/path/to/your/project`), then `Maven` will automatically download the `jar` archive from `Maven Central Repository`. This could be **MUCH EASIER** if you are using IDE(i.e., IntelliJ IDEA), the only thing you need to do is click the refresh button of `Maven`.

If you are restricted using the Internet, and have to make `Maven` offline, you could follow the following steps.

1. Download the `jar` file from any place you can get and transfer the `jar` files to your work computer.
2. Move the `jar` files to your local `Maven` Repository as the path of `/path/to/maven_local_repo/cn/org/codecrafters/simple-jwt-facade/`.

### If you are using `Gradle`

Add this module to your project with `Gradle` is much easier than doing so with `Maven`.

Find `build.gradle` in the needed project, and add the following code to the `dependencies` closure in the build script:

```groovy
implementation 'cn.org.codecrafters:simple-jwt-facade:${simple-jwt-facade.version}'
```

### If you are not using `Maven` or `Gradle`

1. Download the `jar` file from the Internet.
2. Create a folder in your project and name it as a name you like(i.e., for me, I prefer `vendor`).
3. Put the `jar` file to the folder you just created in Step 2.
4. Add this folder to your project `classpath`.

## Implement a `TokenResolver`

If you want to use `TokenResolver` to handle with JWTs, you can choose to use any implementation such as `cn.org.codecrafters:simple-jwt-authzero` or any other `simple-jwt-$implementation_artifact`. But if you do choose to use other implementation, it is not the topic we are going to talk about here. We are here for helping you to implement one by yourself.

First, you are going to choose a third-party library or your own library which is aims to process JWTs(i.e., `com.auth0:java-jwt` and `io.jsonwebtoken:jjwt`). Then, you need to confirm which class they are going to use for a parsed JWT(i.e., `DecodedJWT` is being used in `com.auth0:java-jwt`). And let me use `com.auth0:java-jwt` for example in this tutor.

Then, you can add these following codes in your project:

```java
class Auth0TokenResolver implements TokenResolver<DecodedJWT> {
    // Dont forget to implement methods in interface TokenResolver.
}
```

After doing all these, an implemented `TokenResolver` is ready to process JWTs.

**Let's pretend that you already implemented a `TokenResolver` and named as `ImplementedTokenResolver`.**

You will need an instance of the implementation to process JWTs.

```java
var tokenResolver = new ImplementedTokenResolver(/* arguments you declared */)
```

## Create a JSON Web Token with `TokenResolver`

Then, there are 3 method to create a token:

```java
String createToken(java.time.Duration expireAfter, String audience, String subject);

String createToken(java.time.Duration expireAfter, String audience, String subject, Map<String, Object> payloads);

<T extends TokenPayload> String createToken(java.time.Duration expireAfter, String audience, String subject, T payload);
```

## Read or Verify a JSON Web Token

There are many ways to read a JWT.

If you want to read as the data class which is designed by the third-party library, you can just use `resolve(String token)`. If you want know what is contained in this JWT, you can use `extract(String, Class<?>)`.

Meanwhile, the `resolve(token)` method also serves as a token validation mechanism. If any issues arise, such as token expiration, tampering suspicion, or mismatched token signatures, corresponding exceptions will be thrown.

## Renew a Token that is About to Expire

When a token is about to expire, its validity period can be extended using this method, allowing users to obtain a new valid token without the need for re-login.

**Renew a token** means that the content of the pre-defined properties by JWT, such as the audience (aud) representing the recipient of this token, will not be altered, except for the time-related fields.

```java
String renew(String oldToken, Map<String, Object> payload);
```

This method allows you to pass new custom payload into the updated token. The new token will be available for 30 minutes.

```java
String renew(String oldToken, Duration expireAfter, Map<String, Object> payload);
```

This method allows you to pass new custom payload into the updated token. The new token will be available for the specific duration.

```java
<T extends TokenPayload> String renew(String oldToken, Duration expireAfter, T payload);
```

This method allows you to pass new custom payload into the updated token. The new token will be available for 30 minutes.

```java
<T extends TokenPayload> String renew(String oldToken, Duration expireAfter, T  payload);
```

This method allows you to pass new custom payload into the updated token. The new token will be available for the specific duration.

## Handle Enum Value in Base Types

JWT 原生不支持处理枚举值，因此需要将这些枚举值数据转换为基础数据类型进行处理。通过给数据的枚举值字段上标记 `@TokenEnum` 注解，并配置属性 `propertyName` 和 `dataType`。属性 `propertyName` 表示该枚举字段作为基础数据类型的字段，属性 `dataType` 表示需要用什么基础数据类型来表示该枚举字段，例如有如下枚举值：
```java
public enum SampleEnum {
    SAMPLE_ENUM_1(1),
    SAMPLE_ENUM_2(2),
    ;
    
    private final Integer code;
    
    public Integer getCode() {
        return code;
    }
    
    SampleEnum(Integer code) {
        this.code = code;
    }
}
```

例如现在有下面的 `Payload Class`：

```java
public class SampleModel implements TokenPayload {
    private String sampleStringValue;
    private Integer sampleIntegerValue;
    private SampleEnum sampleEnumValue;
    
    // getters and setters...
}
```

如果您的类需要将上述枚举值作为整形数据进行处理，那么 `propertyName` 应该为 `code`，而 `dataType` 应该为 `cn.org.codecrafters.simplejwt.constants.TokenDataType.INTEGER`。

在枚举值类型的输出方面，您仅需根据 `propertyName` 实现其对应的 `getter`；如果您需要根据基础类型转换为对应的枚举值，您需要实现一个静态的 `loader` 方法，该方法的签名应该为：

```java
public static <EnumValueClass> loadBy<PropertyName>(<DataTypeClass> value);
```

该 `EnumValueClass` 为类中的枚举值的类名；`PropertyName` 为 `@TokenEnum` 标注中 `propertyName` 的大驼峰表示；`DataTypeClass` 为 `@TokenEnum` 标注中 `dataType` 枚举值所对应的类；以上面的 `Payload Class` 为例，则对应的 `loader` 代码如下：

```java
public static SampleEnum loadByCode(Integer value) {
    // return the mapped enum value by integer value.
}
```

## Contact

If you have any suggestions, ideas, don't hesitate contacting us via [GitHub Issues](https://github.com/CodeCraftersCN/jdevkit/issues/new) or [Discord Community](https://discord.gg/NQK9tjcBB8). 

If you face any bugs while using our library and you are able to fix any bugs in our library, we would be happy to accept pull requests from you on [GitHub](https://github.com/CodeCraftersCN/jdevkit/compare).