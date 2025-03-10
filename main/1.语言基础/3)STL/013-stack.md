# stack

## 简介

栈是基本的数据结构之一,特点是先进后出,就如开进死胡同的车队,先进去的只能最后出来.

在c++ 中,stack的头文件是

```
#include<stack>
```

## stack常用操作

```
stack<int> q;	//以int型为例
int x;
q.push(x);		//将x压入栈顶
q.top();		//返回栈顶的元素
q.pop();		//删除栈顶的元素
q.size();		//返回栈中元素的个数
q.empty();		//检查栈是否为空,若为空返回true,否则返回false
```

时间复杂度都为O(1)

stack不能遍历
