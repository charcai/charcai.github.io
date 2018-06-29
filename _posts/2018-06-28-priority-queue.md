---
layout: post
title: C++ STL之priority_queue优先队列
categories: STL C++
tags: STL C++
---
# 介绍
priority_queue, 又称优先队列，是C++ STL库的重要组成部分之一。  
priority_queue的定义在头文件`<queue>`中，因此需要:
```cpp
#include <queue>
```
它允许用户为队列中元素设置优先级，放置元素的时候不是直接放到队尾，而是放置到比它优先级低的元素前面，标准库默认使用 < 操作符来确定优先级关系。

它的原型是
```cpp
template <class T, class Container = vector<T>,
  class Compare = less<typename Container::value_type> > class priority_queue;
```
其中第一个为元素类型；第二个为承载优先队列的容器类型，一般是vector；第三个是比较函数。但由于后两个已经带有默认值，所以一般使用时只需要`priority_queue<int>`这样就行了。

注：优先队列的优先级关系为值大的优先级高、值小的优先级低，而优先级高的放在队列前面，所以对于默认类型，它的内部元素总是从大到小的。  
# 常用操作
- 压入: `push()`  
- 弹出: `pop()`  
- 取队首元素: `top()` //与一般的队列不一样，不用`front()`  
- 判空: `empty()`  
- 取大小: `size`  
# 样例程序
## 系统类型
```cpp
//程序1
#include <queue>
#include <iostream>
using namespace std;
priority_queue<int> q;
int main()
{
    q.push(1);
    q.push(5);
    q.push(3);
    q.push(9);
    q.push(2);
    cout << q.size() << endl;
    while(!q.empty())
    {
        cout << q.top() << " ";
	    q.pop();
    }
    cout << endl;
    return 0;
}
```
这段程序的输出是：
```bash
5
9 5 3 2 1
```  
## 自定义类型  
使用自定义类型，就要重载`<`运算符了。

例:
```cpp
//程序2
#include <queue>
#include <iostream>
using namespace std;
struct node
{
	int value;
	bool operator < (node x) const //const不能少
	{
		return this -> value < x.value;
	}
	node(int _v): value(_v) {}
};
int main()
{
	priority_queue<node> q;
	q.push(node(3));
	q.push(node(5));
	q.push(node(10));
	cout << q.size() << endl;
	while(!q.empty())
	{
		node tmp = q.top();
		q.pop();
		cout << tmp.value << " ";
	}
	cout << endl;
	return 0;
}
```
输出：
```bash
3
10 5 3
```

# 改变优先级
## 系统类型
很多时候，我们需要由小到大排序，这时候就需要这样：
```cpp
priority_queue<int, vector<int>, greater<int> >pq;
//三个int要一致！
```

注：最后两个`>`号千万不要写在一起，否则有可能被编译器误认为是`>>`运算符！

如果以这行代码替换上面程序1里的定义的话，运行结果就会是这样：
```bash
5
1 2 3 5 9
```
## 自定义类型
自定义类型也是一个道理，但要重载`>`运算符：
```cpp
struct node
{
	int value;
	bool operator > (node x) const
	{
		return this -> value > x.value;
	}
	node(int _v): value(_v) {}
};
priority_queue<node, vector<node>, greater<node> > q;
//三个node也要一样！
```
替换程序2相关内容，输出：
```bash
3
3 5 10
```
