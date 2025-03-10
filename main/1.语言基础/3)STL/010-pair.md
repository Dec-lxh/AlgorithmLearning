# pair

在C++中，pair是一个模板类，用于表示一对值的组合。

```
template<class T1, class T2>
struct pair {
	T1 first; // 第一个值
	T2 second; // 第二个值
	// 构造函数
	pair();
	pair(const T1& x, const T2& y);
	// 比较运算符重载
	bool operator==(const pair& rhs) const;
	bool operator!=(const pair& rhs) const;
	// 其他成员函数和特性
	//...
}
```

pair类模板有两个模板参数，T1和T2，分别表示第一个值和第二个值的类型

pair类模板有两个成员变量，first和second，分别表示第一个值和第二个值

使用pair类可以方便地将两个值组合在一起，并进行传递、存储和操作

## pair嵌套

## pair自带排序规则
