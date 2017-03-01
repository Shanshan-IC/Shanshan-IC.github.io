---
layout:     post
title:      "Stack Implementation in Python"
category:   Algorithms
tags:       Algorithms
---
* content
{:toc}

Two ways to implement stack.

## Codes
```c
#include <iostream>
using namespace std;

class Stack {
private:
    int size;
    int top;
    int *data;
public:
    Stack(int _s){
        top = 0;
        size = _s;
        data = new int[_s];
    }
    bool isempty(){
        return size==0;
    }
    
    bool isFull() {
        return top==size;
    }
    
    void push(int x) {
        if (isFull())
            return;
        data[top] = x;
        top++;
    }
    
    void pop() {
        if (isempty())  return;
        top--;
    }
};

int main() {
    Stack *s = new Stack(19);
    cout << s->isempty() << endl;
    s->push(2);
    cout << s->isempty() << endl;
    s->pop();
    cout << s->isempty() << endl;
    return 0;
}
```


Two queue Implement stack

```C++
#include <queue>
using namespace std;

class stack {
private:
    queue<int> q;
public:
    bool empty() {
        return q.empty();
    }
    void push(int x) {
        q.push(x);
        for (int i=0; i<q.size()-1; i++) {
            q.push(q.front());
            q.pop();
        }
    }
    int top() {
        return q.front();
    }
    void pop() {
        q.pop();
    }
};
```