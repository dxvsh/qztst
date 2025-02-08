---
title: Stacks
description: 
tags: 
share: "true"
---

A stack is a data structure that operates in the **Last In First Out** (LIFO) manner, i.e. the last element to go into the stack is the first one to come out. Each new element you add goes to the top of the stack and when you want to pop off an element from the stack, the one that is currently on top is returned.

An **important observation** on stacks:
- Observe that a stack returns elements in the exact reverse order of which they went in. For example: say you push `a`, `b`, `c` onto  a stack but when you pop the stack, you first get `c`, then `b` and finally `a`.
- So elements are returned in the order opposite to which they went in.
- Thanks to this property, a **stack** can be used to ***reverse a sequence***. You push a sequence into a stack and on popping you get the sequence in the reverse order.

A stack needs to implement the following operations:
- Push : Push an element on to the stack (it will go on top)
- Pop : Retrieve and return the element on top of the stack (the topmost element is removed and returned)
- Peek/Top : Just look at the element on top of the stack without removing it

The time complexities of these operations are as follows:

| Operation | Time Complexity |
| --------- | --------------- |
| Push      | $O(1)$          |
| Pop       | $O(1)$          |
| Peek/Top  | $O(1)$          |

A stack can be easily implemented using a [[Arrays#^fe87f8|Dynamic Array]].

```python
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, n):
        self.stack.append(n)

    def pop(self):
        return self.stack.pop()
    
    def peek(self):
        return self.stack[-1]

	def __repr__(self):
		return f"{self.stack}"
```



