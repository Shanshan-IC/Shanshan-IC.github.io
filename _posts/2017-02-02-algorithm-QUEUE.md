---
layout:     post
title:      "Queue Implementation in Python"
category:   Algorithms 
tags:       Algorithms
---

* content
{:toc}

```cpp
#include <iostream>
using namespace std;

template <typename T>

struct node {
    T data;
    node *next;
    node(T &d){
        data = d;
        next = NULL;
    }
};

template <typename T>
class Queuei {
private:
    int size;
    node<T> *front;
    node<T> *rear;
public:
    Queuei(T &n) {
        node <T> *p = new node<T>(n);
        size = 0;
        front = p;
        rear = p;
    }
    
    int getQueueSize() {
        return size;
    }
    
    bool isEmpty() {
        return size==0;
    }
    
    void push(T n) {
        node<T> *p = new node<T>(n);
        rear->next = p;
        rear = p;
        size++;
    }
    
    void pop() {
        if (size==0)    return;
        node<T> *p = front->next;
        front->next = p->next;
        delete p;
        size--;
    }
   
};

int main() {
    int head = 0;
    Queuei<int> * q = new Queuei<int>(head);
    q->push(2);
    q->push(3);
    cout << q->getQueueSize() << endl;
    q->pop();
    return 0;
}
```

Using two stack to implement one queue

```cpp
#include <stack>

using namespace std;

class Queuei {
private:
    stack <int> s1;
    stack <int> s2;
    
public:
    bool isEmpty() {
        return s1.empty() && s2.empty();
    }
    
    void push(int x) {
        s1.push(x);
    }
    
    int pop() {
        if (s2.empty()) {
            while (!s1.empty()) {
                s2.push(s1.top());
                s1.pop();
            }
        }
        return s2.top();
    }
};

```
