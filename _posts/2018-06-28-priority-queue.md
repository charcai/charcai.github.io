---
layout: post
title: C++ STL之priority_queue优先队列
categories: STL C++
tags: STL C++
---
## 介绍
priority_queue, 又称优先队列，是C++的STL库的重要组成部分之一。  
priority_queue的定义在头文件`<queue>`中，因此需要:
```cpp
#include <queue>
```
它允许用户为队列中元素设置优先级，放置元素的时候不是直接放到队尾，而是放置到比它优先级低的元素前面，标准库默认使用 < 操作符来确定优先级关系。  
它的原型是
```cpp
template <class T, class Container = vector<T>,
  class Compare = less<typename Container::value_type> > class priority_queue;
Priority queue
```
其中第一个为元素类型；第二个为承载优先队列的容器类型，一般是vector；第三个是比较函数。但由于后两个已经带有默认值，所以一般使用时只需要`priority_queue<int>`这样就行了。  
注：优先队列的优先级关系为值大的优先级高、值小的优先级低，而优先级高的放在队列前面，所以对于默认类型，它的内部元素总是从大到小的。  
## 基本使用
- 压入: `push()`  
- 弹出: `pop()`  
- 取队首元素: `top()` //这与一般的队列不一样，不用`front()`  
- 判空: `empty()`  
样例程序
```cpp
priority_queue<int> q;
q.push(1);
q.push(5);
q.push(3);
q.push(9);
q.push(2);
while(!q.empty())
{
    cout << q.top() << endl;
	q.pop();
}
```
