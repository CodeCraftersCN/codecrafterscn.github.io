# Changelog

## [1.1.0](https://github.com/CodeCraftersCN/jdevkit/releases/tag/v1.1.0) - **19 Sept, 2023**

## Features

- Added `PropertyGuard` to protect your configuration properties which will be used by Spring Boot application from being exposed to the public.
> Note:
> This feature is extracted from [**MyBatis-Plus**](https://github.com/baomidou/mybatis-plus), designed by **hubin** (according to the commit histories, he might be [**@qmdx**](https://github.com/qmdx)).
> You are able to see the original page about this feature at [**this link**](https://baomidou.com/pages/e0a5ce/).

## Docs

Optimised javadocs.

## Breaking Changes

- The order of the parameters in initialising `SnowflakeGuidCreator` has been changed to `long dataCentreId, long workerId[, long startEpoch]`, please note that the location exchange of parameter `dataCentreId` and `workerId`.

## Note

The Chinese translations will be applied before **26 Sept, 2023**.

## [1.0.1](https://github.com/CodeCraftersCN/jdevkit/releases/tag/v1.0.1) - 28 Aug 2023

### Fixes

- Fixed the application is unable to start when adding one or several `GuidCreator`s manually to the application.

## [1.0.0](https://github.com/CodeCraftersCN/jdevkit/releases/tag/v1.0.0) - 23 Aug 2023

Nothing is changed in this update.

## [1.0.0-RC](https://github.com/CodeCraftersCN/jdevkit/releases/tag/v1.0.0-RC) - 15 Aug 2023

Nothing is changed in this update.

## [1.0.0-beta](https://github.com/CodeCraftersCN/jdevkit/releases/tag/v1.0.0-beta) - 12 Aug 2023

### Changes

- The developer id in `pom.xml` file has been changed.
- The spring version has been set to `6.0.9`.

## [1.0.0-alpha](https://github.com/CodeCraftersCN/jdevkit/releases/tag/v1.0.0-alpha) - 8 Aug 2023

### Removals

- Removed module `web-dev-suite` due to the same features with Spring Framework.