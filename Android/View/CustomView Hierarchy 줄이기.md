## View Hierarchy

```kotlin
class CustomView @JvmOverloads constructor(
    context: Context,
    attrs: AttributeSet? = null,
    defStyleAttr: Int = 0
) : ConstraintLayout(context, attrs, defStyleAttr) {
	private val binding = ViewCustomViewBinding.inflate(...)
}
```

```kotlin
<androidx.constraintlayout.widget.ConstraintLayout ...
    android:layout_width="@dimen/customview_width"
    android:layout_height="@dimen/customview_height">
	...
</androidx.constraintlayout.widget.ConstraintLayout>
```

위와 같은 형식으로 종종 CustomView 를 만드는데, 실제로 이와 같이 할 경우 ConstraintLayout 안에 binding.root 를 addView 시켜 필요없는 1-depth 가 추가된다.

```kotlin
<merge ...
    tools:parentTag="androidx.constraintlayout.widget.ConstraintLayout">
```

이 때 위와 같이 merge 태그를 사용하면 쓸모없는 depth 를 줄일 수 있다.

그러나 코스트 대비 얻을 수 있는 이점이 적다. 또한, xml 안에서 root 의 LayoutParams 를 정의할 수 없게 된다.

그러나 root 의 onMeasure 을 override 할 수 있다는 강력한 장점이 있다.

---

### 참고
    
[https://pluu.github.io/blog/android/2020/08/16/widget-include-merge/](https://pluu.github.io/blog/android/2020/08/16/widget-include-merge/)
