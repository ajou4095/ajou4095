# Enum Class

Enum Class 는 서로 연관된 상수들을 묶어 정의한 클래스이다.

# Sealed Class

Sealed Class 는 해당 클래스를 상속받은 클래스가 해당 클래스의 하위 클래스로만 존재하는 클래스이다.

# Difference

Enum Class 와 Sealed Class 는 둘다 아이템을 나열한다는 공통점이 있지만, Sealed Class 는 확장가능 (enum extension) 하기 때문에, 더 다양한 상황에 유연하게 대처할 수 있다.

그 예시로 던전 종류를 정의하는 클래스를 들 수 있다. 일반적으로는 던전의 종류를 나열하기 때문에 Enum Class 가 적절하지만, 특수 던전임을 정의할 경우 Sealed Class 를 이용하여 특수 던전들을 하위로 나열할 수 있다.
