---
layout:     post
title:      Data Structures Intro
author:     Nia
tags: 		  CS50 C Data
subtitle:  	Daily Review
category:   daily
---

Lecture day for [CS50](https://niamurrell.github.io/search/index.html#CS50). This week it's all about data structures, and we learned a few types:

* Linked Lists (singly-linked & doubly-linked)
* Stacks
* Queues
* Trees (an specifically, binary search trees)
* Hash tables
* Tries (aka reTRIEvals)

And here are some of the related `struct`s:

### Linked List
A chain of nodes which point to other nodes, held together by a `start` pointer at the beginning and a `NULL` termination at the end. Nodes are recursive, i.e. call other nodes within the node, until `NULL` is reached. Linked lists of nodes are useful because you don't need to know how much memory to allocate before creating the list, unlike an array of data, where if it turns out you need more memory, you have to do a lot of extra work to copy & redefine the array. With linked lists you can expand more freely. 

Linked lists can be **singly-linked** so that the nodes all call `next` in the same direction, or they can be **doubly-linked** so that each node points both forwards and backwards.


Definition of a singly-linked node struct:
```C
typedef struct node {
	int n;
	struct node *next;
} node;
```

Definition of a doubly-linked node struct:
```C
typedef struct node {
	int n;
	struct node *prev;
	struct node *next;
} node;
```

To search a linked list, go through each node (first the int `n` then `next` to the next node) until you find the value you're looking for:
```C
bool search(int n, node *list)
{
	node *ptr = list;
	while
	{
		if (ptr -> n == n)
		{
			return true;
		}
		ptr = ptr -> next;
	}
	return false;
}
```

### Stacks

Data is stored vertically so that you can only retrieve the last node added to the stack (LIFO: last in, first out). Stacks can be altered with `push` (add data) or `pop` (remove data). `Top` should be defined as a global variable so that it always lets you reference the last node added to the stack. Definition of a stack struct:
```C
typedef struct {
	int *numbers;
	int size;
} stack;
```

### Queues

Data is stored in a line and you always retrieve data from the front of the line (FIFO: first in, first out). Queues can be altered when you `enqueue` a node at the end of the line or `dequeue` a node from the front of the line. A `front` variable is maintained to store the current location of the front of the queue. `Size` also needs to be kept track of. Definition of a queue struct:
```C
typedef struct {
	int front;
	int *numbers;
	int size
} queue;
```

### Trees

Data is stored cascading from a `root node` in `children`; any node without children are `leaves`. In a **binary search tree** each node as `0`, `1`, or `2` children; the left child is always smaller than its parent and the right child is always bigger. This way you can easily throw out whole branches of data as you traverse the tree. It's important for the tree to be balanced (i.e. not to heavy on one side or another) to ensure big O run time optimization. Definitions of a tree struct:
```C
typedef struct {
	int n;
	struct node *left;
	struct node *right;
} node;
```
For compression:
```C
typedef struct node {
	char symbol;
	float frequency;
	struct node *left;
	struct node *right
} node;
```

To search a binary tree:
```C
bool search(int n, node *tree)
{
	if (tree == NULL)
	{
		return false;
	} 
	else if (n < tree -> n)
	{
		return search(n, tree -> left);
	}
	else if (n > tree -> n)
	{
		return search(n, tree -> right);
	}
	else 
	{
		return true;
	}
}
```

### Hash Tables

With good design hash tables can have more efficiency than the above methods in terms of running time. Using a hash table is like splitting the data into buckets in a consistent manner, so that you have to search smaller collections of data when you're looking for something. Each bucket is a **linked list** of the inner data.

### Tries

An even more efficient style of hash table to reduce the running time greatly. With this recursive system, each bucket contains the same buckets as the parent level, and data are stored by traversing bucket by bucket until reaching an `end` marker. For example to store words, each bucket on the parent level would represent a letter `A - Z`, and then in each of those buckets are additional buckets `A - Z`. To find a word you follow the buckets one inside the next for each letter, until you determine the end of the word.