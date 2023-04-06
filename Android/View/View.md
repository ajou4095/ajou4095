# View 가 그려지는 흐름

1. View 를 Window 에 attach 한다.
- onAttachedToWindow
2. View 의 크기를 측정한다. (= measure pass)
- onMeasure (`measuredWidth`, `measuredHeight` 값을 설정한다.)
- `measuredWidth`, `measuredHeight` 를 바탕으로 `width`, `height` 를 설정한다.
3. View 를 배치한다. (=layout pass)
- onLayout
4. 그린다.
- onDraw

![image](https://user-images.githubusercontent.com/48707913/230285959-635243bc-57f0-446f-b017-b5c12e42aead.png)

Activity/Fragment 의 (onCreate/onViewCreated), onStart, onResume 에서 View 의 크기를 가져오려고 해도 가져오지 못한다.

onResume 이후에 measure pass 가 진행되기 때문이다.

만약 필요하다면 doOnLayout 을 사용해야 한다.

# onMeasure, onLayout

measure(widthMeasureSpec, heightMeasureSpec) 로 측정을 명령하면 onMeasure 에서 실제로 측정을 진행한다.

measureSpec 는 size 와 mode, 두가지의 정보를 담고 있으며, 아래와 같은 관계를 가지고 있다.

```
measureSpec = MeasureSpec.makeMeasureSpec(size, mode)

size = MeasureSpec.getSize(measureSpec)
mode = MeasureSpec.getMode(measureSpec)
```

- MeasureSpec.UNSPECIFIED : 자유롭게 사이즈를 측정함.
- MeasureSpec.EXACTLY : 사이즈를 고정함.
- MeasureSpec.AT_MOST : 최대 사이즈를 지정함.

만약 onMeasure 을 직접 구현할 시, setMeasuredDimension 을 통해 measuredWidth, measuredHeight 를 지정해주어야 한다.

이후 measuredWidth, measuredHeight 를 기반으로 실제로 그려질 width, height 가 만들어지며, 이는 measuredWidth, measuredHeight 와 사이즈가 다를 수 있다.

onLayout 에서는 View 의 layoutParam (margin, etc..) 에 따라서 배치가 이루어진다.

# requestLayout & invalidate

requestLayout : onMeasure, onLayout 을 다시 진행하며, 부모 / 자식 뷰에도 영향을 미친다.

invalidate : onDraw 를 다시 진행한다.
