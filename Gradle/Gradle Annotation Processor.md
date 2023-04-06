# annotationProcessor

annotationProcessor 은 컴파일 타임에 Annotation 을 읽어 code generation 을 진행시키는 도구이다.

- Target Language : Java
- Code Generation : Java 코드를 만들어 연결한다.

# kapt

kapt 는 kotlin annotation processing tool 의 약자로, annotationProcessor 과 동일하게 컴파일 타임에 Annotation 을 읽어 code generation 을 진행시키는 도구이다.

- Target Language : Kotlin
- Code Generation : Java Stub 코드를 만들어 연결하고, 실제 annotation processing phase 가 종료되면 Kotlin code 가 만들어진다.

annotationProcessor 은 Java code generation 을 하기 위한 툴이었기 때문에 기존 라이브러리를 그대로 이용할 경우 kotlin 파일을 만들어 낼 수 없었다.

이러한 이유 때문에 Kotlin 프로젝트와 Java 기반 annotation processor 과의 호환성을 보장하기 위해 중간코드로 Java Stub 을 생성한다.

# ksp

ksp 는 kotlin symbol processing 의 약자로, annotationProcessor 과 동일하게 컴파일 타임에 Annotation 을 읽어 code generation 을 진행시키는 도구이다.

- Target Language : Kotlin
- Code Generation : Java Stub 코드를 만들지 않고, Kotlin 코드를 만들어 연결한다.

ksp 는 Kotlin code generation 을 하기 위한 툴이기에 라이브러리 차원에서 어떻게 코틀린 파일을 생성할지 결정해야 한다. 따라서 라이브러리가 지원해주지 않으면 ksp 를 사용할 수 없다.

Java Stub 코드를 만들지 않기 때문에 kapt 보다 가볍고 빠르며 효율적이다.
