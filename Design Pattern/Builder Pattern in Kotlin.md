# 1. ������ ����

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

���� ���� ��Ȳ���� subTitle �� �߰��ش޶�� ��û�� ���Դ�.

```kotlin
showModal("����", "�޼���")
```

�׷��� �ش� �޼ҵ带 ���� ���� ����ϴ� ���� ����, subTitle �� �߰��ϴ� �� ���ε� �ش� �޼ҵ带 ����ϴ� ��� ���� ������ ��ġ�� ��Ȳ�� ���ܹ��ȴ�.

���� subTitle ���Ŀ��� detailMessage, icon, onDismiss ��� �߰����� ��û�� ���� ���, ���������� ����ϰ� �ִ� ��� ���� ������ ��ġ�� �ȴ�.

�̴� ����� �����ִ� ����� ������ ������ ��� showModal �� �����Ǿ�� �ϹǷ� ���濡 �����ֱ⿡ OCP �����̴�.

# 2. Builder ����

---

�̿� ���� �����ڰ� ������ ��� Builder ������ �̿��� ������ �ذ��Ѵٰ� �Ѵ�.

Builder ������ ����� ���

- ���� ���������� ���� �����ϴ�.
- �ʿ��� Parameter �� ���� �����ϴ�.

```kotlin
ModalBuilder.newInstance()
	.setTitle("����")
	.setMessage("�޼���")
	.show()
```

���� ���� ��� ��� ��� ���� ���� ����� ����ߴٸ�, subTitle �� �߰��ϴ��� �ش� �ڵ�� ������� �����Ƿ� OCP �� �ؼ��ϰ� �ȴ�.

# 3. �̰� �³���?

---

�� �ڵ�� Kotlin �� ��� Ư���� ���� Ȱ���ϰ� ���� ���� �ڵ��̴�.

Kotlin �� named argument �� default value �� �̿��ϸ� �ش� ������ �ذ��� �� �ִ�.

�׷��� named argument �� ��� ����� �������̶�, ����ϴ� ������ named argument �� ������� ���� �� �ְ�, �� ��� ������ ������ �ذ��� �� ����. �׷� ��� Kotlin �� ��� Ư���� Ȱ������ ���ϴ���, ���濡 ������ �ϱ� ���� Builder ������ ����ϴ� ���� ��ü���� �������� �ùٸ��ٰ� �����ߴ�.

�׷��� �ش� ������ ������ ������ �ƴ� ������ ������ ���� �ڷ���� ã�ƺ��Ұ�, ��� ���� �ش��� ã�Ҵ�.

# 4. Named Argument �� ����

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

�� ���̺귯���� �̿��� ��� named argument �� ������ �� �ִ�.

���������� �̴� ��� �󿡼� ��������� �ϴ� �����̶�� �����ϸ�, �������� �������� ����� ������ ����ν�� ũ�� ���� ����� �ƴ϶�� �����Ѵ�.

������ Kotlin ���δ� �Ϻ��ϰ� Builder ������ ��ü�� ���� ������, ���� ����� ����� �� �ִٸ� Kotlin ������ Builder ������ �ʿ� ���ٰ� �����Ѵ�.