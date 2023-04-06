# Extra Proterties Extension

[https://docs.gradle.org/current/dsl/org.gradle.api.plugins.ExtraPropertiesExtension.html](https://docs.gradle.org/current/dsl/org.gradle.api.plugins.ExtraPropertiesExtension.html)

build script 안에서 Version 을 모아서 관리하는 방법이다.

```groovy
project.ext {
    myVersion = "version"
    myProperty = "property"
}
```

# Build Sources

[https://docs.gradle.org/current/userguide/organizing_gradle_projects.html#sec:build_sources](https://docs.gradle.org/current/userguide/organizing_gradle_projects.html#sec:build_sources)

build script 에 존재하던 버전을 모듈로 빼 캡슐화한, 버전 관리법중 하나이다.

```groovy
.
├── buildSrc
│   ├── build.gradle
│   └── src
│       ├── main
│       │   └── java
│       │       └── com
│       │           └── enterprise
│       │               ├── Deploy.java
│       │               └── DeploymentPlugin.java
│       └── test
│           └── java
│               └── com
│                   └── enterprise
│                       └── DeploymentPluginTest.java
├── settings.gradle
├── subprojecto-one
│   └── build.gradle.kts
└── subproject-two
    └── build.gradle.kts
```

# Version Catalog

[https://docs.gradle.org/current/userguide/platforms.html](https://docs.gradle.org/current/userguide/platforms.html)

version catalog 는 build script 에서 사용할 종속성을 나열해놓은 파일이다.

> For each catalog, Gradle generates *type-safe accessors* so that you can easily add dependencies with autocompletion in the IDE.
> 
> 
> Each catalog is visible to all projects of a build. It is a central place to declare a version of a dependency and to make sure that a change to that version applies to every subproject.
> 
> Catalogs can declare [dependency bundles](https://docs.gradle.org/current/userguide/platforms.html#sec:dependency-bundles), which are "groups of dependencies" that are commonly used together.
> 
> Catalogs can separate the group and name of a dependency from its actual version and use [version references](https://docs.gradle.org/current/userguide/platforms.html#sec:common-version-numbers) instead, making it possible to share a version declaration between multiple dependencies.
>
