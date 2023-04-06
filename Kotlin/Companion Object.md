# Companion Object

Companion Object 는 클래스 안에 존재하는 싱글톤 객체이다.

Java 에서 구현될 때에는 다음과 같다 :

Companion Object 는 클래스 안에 Nested Class 로 존재하며, 클래스 안에 Companion Object instance 로 Companion 이라는 객체가 만들어지며, 이는 클래스가 로딩될 때 만들어진다.

이 Companion Object 의 객체명/클래스명을 임의로 변경할 수 있고, 상속받을 수 있다.
