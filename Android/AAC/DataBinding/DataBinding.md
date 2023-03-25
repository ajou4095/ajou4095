# DataBinding
---
layout xml ���� ������ ������� �����͸� Observe �� �ݿ��ϰ� ���ִ� AAC ���̺귯���̴�.

### ����
---
- ������ ����
  Activity / Fragment �� View ������Ʈ å���� �и��� �� �ִ�.
  - SRP : Activity �� System ���� å�Ӹ��� ���� �� �ֵ��� �����ش�.
  - OCP : �����͸� notify �ϴ� �������� �κ��� �������� ������, notify �� �޾��� ���� ���� �ൿ�� �߻�ȭ�ȴ�. ���� �����͸� ��� �����ϰ� ��� ������Ʈ�ϴ����� ���� �κи� �ۼ��ϸ� �ȴ�.
- ������ ���α׷���
  xml ���� ��� View �� ���� ������Ʈ ������ ������ �־� ȭ�鿡 ���� ������ ��������.
  - SRP : xml ������ View�� � ������Ʈ�� �ؾ��ϴ����� ���� å���� ������, BindingAdapter/BindingMethod ���� ���� ������ ���� å���� ��������.

### ViewBinding
---
Activity / Fragment ���� View �� ���� ������ �ؾ��� ��, �������� View�� ID �� ���� ã�ƿ;� �ߴ�. (`findViewById`)
ViewBinding �� �̿��� xml�� �ڵ�� ������ ViewDataBinding ��ü�� ���� �� �ִ�.
�̸� �̿��� �˻����� �ʰ� ���� View �� ���� ������ ����������, �̿� ���� View �� �� ������, null-safety �ϰ� ������ �� �ְ� �Ǿ���.
ViewBinding �� DataBinding �� �����ִ� ���̺귯����.
���� DataBinding ��� �� ViewBinding �� ����� �� ������, ViewBinding ���� ���� ����� ���� �ִ�.

### ���� ���� ���
---
```
buildFeatures {
    dataBinding = true
}
```
Gradle ���� ���� ���� `dataBinding = true` �ɼ��� �ָ� ���Ӽ� �߰��� �ȴ�.
Application ��⿡�� ���� ������ DataBinderMapper �� ��� �����ϱ� ������,
library ��⿡�� DataBinding �� ����� ��� �ش� ��� ���Ӽ��� ������ �ִ� ��� ���� ������ DataBinding Ȱ��ȭ�� �ؾ� �Ѵ�.

### ����
---
xml ���� �ֻ���� <layout> �±׷� ���� DataBinding �� ����� �� �ִ�.

### �����ϴ� �Ǽ�
---
- DataBinding Event Listener
> BindingAdapter / BindingMethod �� lambda function�� ���� ���, �׸��� �� xml ���� �ΰ� �̻��� lambda function BindingAdapter / BindingMethod �� ������ ��� ���� ������ �߻��Ѵ�.
[���� ��ũ](!https://stackoverflow.com/questions/54692274/android-data-binding-problem-missing-return-statement-in-generated-code-while-u)
DataBinding ���� �̺�Ʈ�� �ڵ鸵�ϰ��� �� ������ lambda function �� �ƴ� interface / abstract class �� �̿��� ������ �Ѵ�.

- DataBinding Kotlin File
> xml ������ java �� ��ȯ�� ���Ͽ� �����ϱ� ������ �����ؾ��Ѵ�.
Companion Object �� ������ ������ .Companion
Object class �� ������ ������ .INSTANCE �� ���� �����;� �Ѵ�.
databinding ������ java�ε�, �̷� ���� DataBinding �� non-nullable �� null ���� ������ NPE �� �߻��Ѵ�.
������ `androidx.databinding.adapters.Converters` �� �ִ� BindingConversion �� ����� ��� ���ο��� null ó���� �ϰ� ���� �ʱ� ������ NullPointerException �� �߻��� �� �ִ�.
�׷��� ���ڴ� DataBinding �� �� ������ �����͸� nullable �ϰ� ���� �� �ֵ��� ����� �� ��õ�Ѵ�.

### Issue
---
- ViewBinding in Module
> �ȵ���̵�� ����Ÿ�ӿ� ��� xml �� ��� �����Ѵ�.
ViewBinding ��ü�� inflate �� �� ����Ÿ�ӿ� Application ��⿡ ��������� `androidx.databinding.DataBinderMapperImpl` �� reflection ���� �����ϴµ�,
�� �� Android Studio Layout Preview ������ �ش� ��ü�� �������� ���Ѵ�.
���� �����ϴ� �ٷδ� layout xml �� ����Ÿ�� �� �ϳ��� ��������, �̸� MergedDataBinderMapper ���� �����ϴµ�,
�� �� ���� ���ø����̼��� ���ư� ���� xml ��ġ�� Layout Preview ������ xml ��ġ�� ����ġ�ϱ� �������� �����ȴ�.
[���� ��ũ](!https://issuetracker.google.com/u/3/issues/268597957)
2023.03.25 ����, Giraffe Canary ������ �ش� ������ ���������� �߻��Ѵ�.