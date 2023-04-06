# Gradle

Gradle 은 프로젝트를 관리하는 툴이다.

Gradle 은 Gradle Script 로 프로젝트를 관리하고, 이를 기반으로 빌드를 돌린다.

### Gradle Script

Gradle Script 는 전반적인 빌드 구성을 정의한 파일이다.

Gradle Script 를 통해서 프로젝트의 구조를 설정하고, 의존성을 관리하고, Task 를 정의할 수 있다.

- build.gradle : 프로젝트의 전반적인 빌드 구성을 정의한다. (dependency, etc...)
- settings.gradle : 멀티 프로젝트의 전반적인 빌드 구성을 정의한다. (repository, module, etc…)
- gradle.properties : Gradle 의 속성을 정의한다. (gradle version, cache option, etc…)

### Gradle Task

Gradle Task 는 Gradle 에서의 작업 단위이다.

Gradle Task 를 통해서 여러 프로세스를 정의하고 자동화할 수 있다.

Gradle Task 는 Gradle Script 에서 정의할 수 있다.

- build : 프로젝트를 빌드한다.
- test : 프로젝트를 테스트한다.
- clean : 빌드 타임에 만들어진 모든 파일을 삭제한다.

### Gradle Plugin

Gradle Plugin 은 Gradle Script 로 구성돼, Gradle Build System 에 새로운 feature 을 수정 및 추가할 수 있다.

Gradle Plugin 은 build.gradle 의 plugins 블록에서 적용시킬 수 있다.

- AGP : Android Application Build feature 가 포함되어 있는 플러그인이다.
- maven-publish : maven repository 에 publish 하는 feature 가 포함되어 있는 플러그인이다.
- enigma : 프로젝트의 모든 String 코드를 빌드 시 암호화하는 feature 가 포함되어 있는 플러그인이다.

# AGP (Android Gradle Plugin)

Android Gradle Plugin 은 Android Application Build Feature 가 포함되어있는 플러그인이다.

Android Gradle Plugin 에는 최소 요구 Gradle Version 이 있으므로 주의해야한다.

[https://developer.android.com/build/releases/gradle-plugin](https://developer.android.com/build/releases/gradle-plugin)

### AGP Task

- assemble : Application 모듈의 경우 APK를, Library 모듈의 경우 AAR / JAR 파일을 만든다.
- bundle : App Bundle 을 만들 수 있다.

---
### Reference
[https://medium.com/@banmarkovic/what-is-gradle-and-why-do-we-use-it-as-android-developers-572a07b3675d](https://medium.com/@banmarkovic/what-is-gradle-and-why-do-we-use-it-as-android-developers-572a07b3675d)
