---
layout:     post
title:      "Leetcode (225, 232) Implement Stack using Queues and Implement" Queue using Stacks
category:   Leetcode 
tags:		Leetcode Stack Queue
---

* content
{:toc}

## Leetcode 225. Implement Stack using Queues
* [Leetcode 225. Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/)

Implement the following operations of a stack using queues.

push(x) -- Push element x onto stack.

pop() -- Removes the element on top of the stack.

top() -- Get the top element.

empty() -- Return whether the stack is empty.

```cpp
class Stack {
public:
    // Push element x onto stack.
    void push(int x) {
        q.push(x);
        for (int i=0; i<q.size()-1; i++) {
            q.push(q.front());
            q.pop();
        }
    }

    // Removes the element on top of the stack.
    void pop() {
        q.pop();
    }

    // Get the top element.
    int top() {
        return q.front();
    }

    // Return whether the stack is empty.
    bool empty() {
        return q.empty();
    }
private:
    queue<int> q;
};
```

## Leetcode 232. Implement Queue using Stacks

* [Leetcode 232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)

Implement the following operations of a queue using stacks.

push(x) -- Push element x to the back of queue.

pop() -- Removes the element from in front of queue.

peek() -- Get the front element.

empty() -- Return whether the queue is empty.

```cpp
class Queue {
public:
    // Push element x to the back of queue.
    void push(int x) {
        input.push(x);
    }

    // Removes the element from in front of queue.
    void pop(void) {
        peek();
        output.pop();
    }

    // Get the front element.
    int peek(void) {
        if (output.empty()) {
            while (!input.empty()) {
                output.push(input.top());
                input.pop();
            }
        }
        return output.top();
    }

    // Return whether the queue is empty.
    bool empty(void) {
        return input.empty() && output.empty();
    }
private:
    stack<int> input;
    stack<int> output;
};
```