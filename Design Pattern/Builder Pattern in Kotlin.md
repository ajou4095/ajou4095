# 1. 봉착한 문제

---

```kotlin
fun showModal(
	title: String? = null,
	message: String? = null,
	isCancelable: Boolean = false,
	onConfirm: (() -> Unit)? = null,
	onCancel: (() -> Unit)? = null
): Unit {
	...
}
```

위와 같은 상황에서 subTitle 을 추가해달라는 요청이 들어왔다.

```kotlin
showModal("제목", "메세지")
```

그러나 해당 메소드를 위와 같이 사용하는 곳이 많아, subTitle 을 추가하는 것 뿐인데 해당 메소드를 사용하는 모든 곳에 영향을 미치는 상황이 생겨버렸다.

또한 subTitle 이후에도 detailMessage, icon, onDismiss 등등 추가적인 요청이 들어올 경우, 마찬가지로 사용하고 있는 모든 곳에 영향을 미치게 된다.

이는 모달을 보여주는 방식이 수정될 때마다 모든 showModal 이 수정되어야 하므로 변경에 열려있기에 OCP 위반이다.

# 2. Builder 패턴

---

이와 같이 생성자가 복잡할 경우 Builder 패턴을 이용해 문제를 해결한다고 한다.

Builder 패턴을 사용할 경우

- 값을 직관적으로 전달 가능하다.
- 필요한 Parameter 만 전달 가능하다.

```kotlin
ModalBuilder.newInstance()
	.setTitle("제목")
	.setMessage("메세지")
	.show()
```

만약 기존 사용 방법 대신 위와 같은 방법을 사용했다면, subTitle 을 추가하더라도 해당 코드는 변경되지 않으므로 OCP 를 준수하게 된다.

# 3. 이게 맞나…?

---

위 코드는 Kotlin 의 언어 특성을 전혀 활용하고 있지 않은 코드이다.

Kotlin 의 named argument 와 default value 를 이용하면 해당 문제를 해결할 수 있다.

그러나 named argument 의 경우 사용이 선택적이라서, 사용하는 곳에서 named argument 를 사용하지 않을 수 있고, 이 경우 기존의 문제를 해결할 수 없다. 그럴 경우 Kotlin 의 언어 특성을 활용하지 못하더라도, 변경에 닫히게 하기 위해 Builder 패턴을 사용하는 것이 객체지향 관점에서 올바르다고 생각했다.

그러나 해당 문제는 나만의 문제가 아닐 것으로 생각해 관련 자료들을 찾아보았고, 어느 정도 해답을 찾았다.

# 4. Named Argument 의 강제

---

[https://youtrack.jetbrains.com/issue/KT-14934](https://youtrack.jetbrains.com/issue/KT-14934)

[https://github.com/chao2zhang/RequireNamedArgument](https://github.com/chao2zhang/RequireNamedArgument)

```kotlin
@NamedArgsOnly
fun buildSomeInstance(param1: Boolean = true, param2: Boolean = false /* so on */)

// Ok
buildSomeInstance(param1 = false, param2 = true)

// Compilation error
buildSomeInstance(false, true)
```

위 라이브러리를 이용할 경우 named argument 를 강제할 수 있다.

개인적으로 이는 언어 상에서 지원해줘야 하는 내용이라고 생각하며, 쓸데없는 의존성이 생기기 때문에 현재로써는 크게 좋은 방식은 아니라고 생각한다.

현재의 Kotlin 으로는 완벽하게 Builder 패턴을 대체할 수는 없지만, 위의 기능을 사용할 수 있다면 Kotlin 에서는 Builder 패턴은 필요 없다고 생각한다.