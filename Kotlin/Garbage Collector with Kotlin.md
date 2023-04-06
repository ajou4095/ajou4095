# About GC

Garbage Collector 은 참조되지 않는 객체를 찾아 메모리에서 해체하는 작업을 말한다.

# Memory in JVM

JVM 에서 메모리는 총 4가지 구역으로 나누어져 있다.

- Heap area - 객체가 저장된다.
- Stack area - 메소드 호출과 지역변수가 저장된다.
- Method area - 클래스, 상수, 메소드 바이트 코드 등이 저장된다.
- Native area - 네이티브 데이터가 저장된다.

GC 는 Heap Area 만을 검색한다.

# Static

static 의 경우 Java 8 이전에는 Method Area 에 만들어졌지만, Java 8 부터는 Heap Area 에 저장된다.

런타임에 만들어지는 모든 객체들은 참조되지 않으면 모두 GC 의 대상이 될 수 있다.

Static 객체들은 Application 이 시작될 때 ClassLoader 에 의해 참조되므로, 일반적으로 GC 의 대상이 되지 않는다.

### Companion Object / Object class

Companion Object 의 instance 인 Companion 객체는 싱글톤으로 static 하게 만들어진다.

Object class 의 instance 인 INSTANCE 객체 또한 싱글톤으로 static 하게 만들어진다.

위 둘은 모두 static 이므로 ClassLoader 에 의해 참조되므로, GC 의 대상이 되지 않는다.
