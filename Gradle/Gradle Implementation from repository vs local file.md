# Implementation

사용자는 Gradle build script (build.gradle) 에서 종속성을 정의할 수 있다.

- `project("module_name")` 을 통해 모듈 종속성을 정의할 수 있다.
- `files("file_path")` 을 통해 로컬 파일 종속성을 정의할 수 있다.
- `groupId:artifactId:versionName` 을 통해 repository 에 존재하는 라이브러리 종속성을 정의할 수 있다.

### Local file VS Remote file (from repository)

Local 파일은 컴파일 된 파일만을 가지고 있고 (jar, aar, etc..)

Repository 를 통해 가져오면 라이브러리 ID, 버전, 종속 등의 메타데이터가 제공된다.

- maven repository - pom.xml 으로 메타데이터를 관리한다.
- ivy repository - ivy.xml 으로 메타데이터를 관리한다.

Repository 를 통해 종속성을 관리하면 위와 같은 메타데이터를 통해 종속관리를 Gradle 이 대신 해주고, 빌드 시간 또한 단축된다.
