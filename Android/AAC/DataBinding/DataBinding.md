# DataBinding
DataBinding 은 layout xml 에서 선언형 방식으로 데이터를 Observe 해 반영하게 해주는 AAC 라이브러리이다.

# 장점
- 옵저버 패턴
  Activity / Fragment 의 View 업데이트 책임을 분리할 수 있다.
  - SRP : Activity 가 System 관련 책임만을 가질 수 있도록 도와준다.
  - OCP : 데이터를 notify 하는 본질적인 부분은 변경하지 않으며, notify 를 받았을 때에 대한 행동이 추상화된다. 따라서 데이터를 어떻게 가공하고 어떻게 업데이트하는지에 관한 부분만 작성하면 된다.
- 선언형 프로그래밍
  xml 에서 모든 View 에 관한 업데이트 로직을 가지고 있어 화면에 대한 예측이 쉬워진다.
  - SRP : xml 에서는 View가 어떤 업데이트를 해야하는지에 대한 책임을 가지고, BindingAdapter/BindingMethod 에서 실제 로직에 관한 책임을 가져간다.

# ViewBinding
Activity / Fragment 에서 View 에 대한 접근을 해야할 때, 기존에는 View의 ID 를 통해 찾아와야 했다. (`findViewById`)

ViewBinding 을 이용해 xml을 코드로 구현한 ViewDataBinding 객체를 만들 수 있다.

이를 이용해 검색하지 않고 직접 View 에 대한 접근이 가능해졌고, 이에 따라 View 를 더 빠르게, null-safety 하게 가져올 수 있게 되었다.

ViewBinding 은 DataBinding 에 속해있는 라이브러리다.

따라서 DataBinding 사용 시 ViewBinding 도 사용할 수 있지만, ViewBinding 만을 따로 사용할 수도 있다.

# 종속 선언 방법
```
buildFeatures {
    dataBinding = true
}
```
Gradle 에서 위와 같이 `dataBinding = true` 옵션을 주면 종속성 추가가 된다.

Application 모듈에서 하위 모듈들의 DataBinderMapper 을 모아 관리하기 때문에,

library 모듈에서 DataBinding 을 사용할 경우 해당 모듈 종속성을 가지고 있는 모든 상위 모듈들은 DataBinding 활성화를 해야 한다.

# 사용법
xml 에서 최상단을 `<layout>` 태그로 묶어 DataBinding 을 사용할 수 있다.

# 자주하는 실수
### DataBinding Event Listener

BindingAdapter / BindingMethod 로 lambda function을 만들 경우, 그리고 한 xml 에서 두개 이상의 lambda function BindingAdapter / BindingMethod 를 연결한 경우 빌드 에러가 발생한다.

[관련 링크](https://stackoverflow.com/questions/54692274/android-data-binding-problem-missing-return-statement-in-generated-code-while-u)

DataBinding 으로 이벤트를 핸들링하고자 할 때에는 lambda function 이 아닌 interface / abstract class 를 이용해 만들어야 한다.

[Android 공식 문서 참고](https://developer.android.com/topic/libraries/data-binding/binding-adapters)

`Event handlers may only be used with interfaces or abstract classes with one abstract method, as shown in the following`

### DataBinding Kotlin File

xml 에서는 java 로 변환된 파일에 접근하기 때문에 주의해야한다.

Companion Object 에 접근할 때에는 .Companion

Object class 에 접근할 때에는 .INSTANCE 와 같이 가져와야 한다.

databinding 문법도 java인데, 이로 인해 DataBinding 시 non-nullable 에 null 값을 전달해 NPE 가 발생한다.

실제로 `androidx.databinding.adapters.Converters` 에 있는 BindingConversion 을 사용할 경우 내부에서 null 처리를 하고 있지 않기 때문에 NullPointerException 이 발생할 수 있다.

그래서 필자는 DataBinding 을 할 때에는 데이터를 nullable 하게 받을 수 있도록 만드는 걸 추천한다.

# Issue
### ViewBinding in Module

안드로이드는 빌드타임에 모든 xml 을 모아 관리한다.

ViewBinding 객체는 inflate 할 때 빌드타임에 Application 모듈에 만들어지는 `androidx.databinding.DataBinderMapperImpl` 에 reflection 으로 접근하는데,

이 때 Android Studio Layout Preview 에서는 해당 객체를 가져오지 못한다.

현재 추측하는 바로는 layout xml 이 빌드타임 때 하나로 합쳐지고, 이를 MergedDataBinderMapper 에서 관리하는데,

이 때 실제 어플리케이션이 돌아갈 때의 xml 위치와 Layout Preview 에서의 xml 위치가 불일치하기 때문으로 추측된다.

[관련 링크](https://issuetracker.google.com/u/3/issues/268597957)

2023.03.25 기준, Giraffe Canary 에서도 해당 문제가 지속적으로 발생한다.
