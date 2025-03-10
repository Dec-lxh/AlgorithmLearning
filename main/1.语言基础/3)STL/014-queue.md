# queue

## 一、定义

queue是一种容器转换器模板，调用#include< queue>即可使用队列类。

## 二、queue初始化

queue<Type, Container> (<数据类型，容器类型>）
初始化时必须要有数据类型，容器可省略，省略时则默认为deque 类型

初始化示例
1：

```
queue<int>q1;
queue<double>q2;  
queue＜char＞q3；
//默认为用deque容器实现的queue；
```

2：

```
queue＜char, list＜char＞＞q1；
//用list容器实现的queue 

queue＜int, deque＜int＞＞q2；
 //用deque容器实现的queue 
```

注意：不能用vector容器初始化queue
因为queue转换器要求容器支持front（）、back（）、push_back（）及 pop_front（），说明queue的数据从容器后端入栈而从前端出栈。所以可以使用deque和list对queue初始化，而vector因其缺少pop_front（），不能用于queue。

## 三、queue常用函数

### 1.常用函数

push() 在队尾插入一个元素
pop() 删除队列第一个元素
size() 返回队列中元素个数
empty() 如果队列空则返回true
front() 返回队列中的第一个元素
back() 返回队列中最后一个元素

时间复杂度都为O(1)

### 2.函数运用示例

1：push（）在队尾插入一个元素

```
queue <string> q;
q.push("first");
q.push("second");
cout<<q.front()<<endl;
```

输出 first

2：pop() 将队列中最靠前位置的元素删除，没有返回值

```
queue <string> q;
q.push("first");
q.push("second");
q.pop();
cout<<q.front()<<endl;
```

输出 second 因为 first 已经被pop（）函数删掉了

3：size() 返回队列中元素个数

```
queue <string> q;
q.push("first");
q.push("second");
cout<<q.size()<<endl;
```

输出2，因为队列中有两个元素

4：empty() 如果队列空则返回true

```
queue <string> q;
cout<<q.empty()<<endl;
q.push("first");
q.push("second");
cout<<q.empty()<<endl;
```

分别输出1和0
最开始队列为空，返回值为1（ture）；
插入两个元素后，队列不为空，返回值为0（false）；

5：front() 返回队列中的第一个元素

```
queue <string> q;
q.push("first");
q.push("second");
cout<<q.front()<<endl;
q.pop();
cout<<q.front()<<endl;
```

第一行输出first；
第二行输出second，因为pop（）已经将first删除了

6：back() 返回队列中最后一个元素

```
queue <string> q;
q.push("first");
q.push("second");
cout<<q.back()<<endl;
```

输出最后一个元素second

# priority_queue

priority_queue中的元素是按照一定的优先级进行排序的。默认情况下，priority_queue按照元素的值从大到小进行排序，大根堆

## 常用函数

push(x)   将元素x插入到优先队列中       O(logN)

pop()       弹出优先队列中的顶部元素     O(logN)

top()	返回优先队列中的顶部元素     O(1)

empty(）检查优先队列是否为空	     O(1)

size()	返回优先队列中元素的个数     O(1)

## 优先队列修改比较函数

(1)仿函数

```
struct Compare{
	bool operator()(int a,int b){    //重载
		//自定义的比较函数，按照逆序排列
		return a<b;
	}
}；
int main(){
	std::priority_queue<int,std::vector<int>,Compare> pq;
}
```

小根堆

(2)

```
auto compare=[](int a,int b){
	//自定义的比较函数，按照逆序排列
	return a<b;
}
std::priority_queue<int,std::vector<int>,decltype(compare)> pq(compare);
```

如果优先队列中的元素类型比较简单，可以直接使用greater<T>来修改比较方法

```
std::priority_queue<int,std::vector<int>,greater<int>> pq;
```

# deque双端队列

双端队列（deque）是队列的一种变形，一般队列只能在队尾添加元素（push），在队首删除元素（pop），双端队列则同时在队首或者队尾执行添加和删除工作。C++中，使用双端队列需要包含头文件<deque>。

## C++中队列的基本操作

| 函数          | 含义                           | 时间复杂度 |
| ------------- | ------------------------------ | ---------- |
| push_back(x)  | 在队尾插入元素x                | 平摊O(1)   |
| push_frontx() | 在队头插入元素x                | 平摊O(1)   |
| pop_back()    | 移除队尾元素                   | 平摊O(1)   |
| pop_front()   | 移除队头元素                   | 平摊O(1)   |
| front()       | 返回队首元素的引用             | O(1)       |
| back()        | 返回队尾元素的引用             | O(1)       |
| empty()       | 判断队列是否为空，空（true）   | O(1)       |
| size()        | 获取队列中元素个数             | O(1)       |
| clear()       | 移出所有的元素，容器大小变为 0 | O(N)       |

