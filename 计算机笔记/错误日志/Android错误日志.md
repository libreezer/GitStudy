## findViewById()找不到自定义View对象的一种原因

```
public AutoLinefeedView(Context context)

public AutoLinefeedView(Context context, @Nullable AttributeSet attrs)
```
以上两个方法都必须被`super()`实现，否则在xml布局中就无法实现view。