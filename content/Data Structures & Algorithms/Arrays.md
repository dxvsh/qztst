---
title: Arrays
description: 
tags: 
share: "true"
---

Arrays represent a ***contiguous*** block/chunk of memory in RAM. You can have two types of arrays: Static Arrays & Dynamic Arrays 

**Static Arrays** : are fixed size arrays that you create during declaration. These cannot grow or shrink over time. They stay the same size as you specified during declaration. If you want to store more elements than the size of the array, then you'll need to allocate a new array of a bigger size in memory.

**Dynamic Arrays** : don't have a fixed size, and can grow overtime. Lists in Python are an example. Initially the language creates a small array (say 5 elements) and when you fill it up, it allocates a new array that is twice the size of the old one (so now, its size will be 10) and copies the elements of the old array to the new one. Now you can continue adding elements to it. When you fill up this array, again a new array (that is 2x the size) is allocated and the elements are copied over to it. This process happens whenever the array runs out of space. ^fe87f8

Lets discuss a few common array operations and their time complexity:

- Reading/Writing an element at the $i$-th index: $O(1)$ 
	- You can access any random element in an array in constant time $O(1)$. So accessing/reading the $i$-th element and replacing/overwriting the $i$-th element are both constant time operations.
- Insertion/Deletion at the end: $O(1)$
	- Inserting and deleting an element at the end of an array is a constant time: $O(1)$ operation 
- Insertion/Deletion at the $i$-th index: $O(n)$
	- Inserting or deleting an element at an arbitrary position in the array is $O(n)$ operation in the worst case because you'll need to shift a whole bunch of other elements to the right or left.

| Operation                            | Time Complexity |
| ------------------------------------ | --------------- |
| Lookup/Overwrite at the $i$-th index | $O(1)$          |
| Insert at the end                    | $O(1)$          |
| Remove from end                      | $O(1)$          |
| Insert at the $i$-th index           | $O(n)$          |
| Remove from the $i$-th index         | $O(n)$          |
The time complexity is the same for both static and dynamic arrays.

Side Note:

- For dynamic arrays, when you want to insert at the end and you've run out of space, a new array is created and the elements from the old are copied over. This is a $O(n)$ operation but after that is done inserting more elements is again just a $O(1)$ operation. 
- But this situation will arise relatively few times. Most of the times you'll just be inserting elements at the end in $O(1)$ time and only when you run out of space, we'll need $O(n)$ for creating a new array. So on average, we'll be mostly performing an $O(1)$ operation instead of $O(n)$. 
- This is why the ***amortized time complexity*** of inserting an element at the end remains $O(1)$ for a dynamic array.