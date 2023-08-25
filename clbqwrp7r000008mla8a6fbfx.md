---
title: "Nearest Smallest Element, Classical Stack Problem"
seoTitle: "Nearest Smallest Element, Classical Stack Problem Explained"
seoDescription: "In this post, we talk through the classical problem: "Nearest Smallest Element" and how to solve it efficiently using a stack."
datePublished: Fri Dec 16 2022 19:33:32 GMT+0000 (Coordinated Universal Time)
cuid: clbqwrp7r000008mla8a6fbfx
slug: nearest-smallest-element-classical-stack-problem
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1671213725881/s18Y8CnzC.png
tags: tutorial, cpp, algorithms, data-structures, competitive-programming

---

## Introduction

Hello Everyone! 👋, welcome back, in this post I want to show you one of my favorite trivial stack problems and some variations, I will explain the problem, go through the most simple but inefficient answer, and then the correct and brilliant solution using stacks.

## Problem

### Statement

Given an Array of positive integers, for each array element output the nearest smaller element, i.e., the first smaller element that comes after the element in the array, if no element exists, output -1.

### Limits

*   N (the size of the array) 1 &lt;= N &lt;= 10^6
    
*   Ai (Element in the array) 1 &lt;= Ai &lt;= 10^6
    

### Examples

```cpp
INPUT:
6
3 2 4 5 1 6
OUTPUT:
2 1 1 1 -1 -1
```

```cpp
INPUT:
3
3 1 2
OUTPUT:
1 -1 -1
```

## Iterative Solution

If you understood the problem then it's very likely that you already thought of this solution, the algorithm is very simple, for each element simply iterate from that position to the end of the array in the search for a smallest element, and if found, immediately output that element, finish the search, and continue to the next item. If not found output -1.

### Code Implementation

Based on the explanation above, I highly recommend that you try to code the solution for yourself, and then compare it to the code implementation below.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
  int n; cin >> n;
  vector<int>arr(n); for(auto &e:arr)cin >> e; // getting input

  for(int i=0; i<n; i++){
    int current = arr[i];
    bool found = false;
    for(int j=i; j<n; j++){
      if(arr[j] < current){cout << arr[j] << " "; found=true; break;}
    }
    if(!found)cout << -1 << " ";
  }
  return 0;
}
```

When I first made this solution, I thought: "Hey! this is a great simple solution let's submit this code!", but that's because I didn't had a great understanding of complexity and efficiency at the time, and I got a TLE verdict 😔.

### Time and Space Complexity

If you have never heard of time and space complexity and Big-O notation, I highly suggest that you read my post: [Efficiency and Big-O Notation Overview](https://blog.garybricks.com/efficiency-and-big-o-notation-overview-with-python-examples)

This code has a time complexity of ***O(n^2)*** and a space complexity of ***O(n)***. The time complexity is determined by the two nested loops, which both run in linear time with respect to the size of the input `n`. The space complexity is determined by the use of the `vector` container, which has a size of `n`.

in the worst case, ***n*** can be 1,000,000, with this algorithm the amount of operations is going to be approximately 1,000,000,000,000 in a worst-case scenario which is why we get a Time Limit Exceeded (TLE) verdict.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670705510379/8lReYEDdq.png align="center")

## Stack Solution

Now that we understand why the iterative solution is not the right choice, let's think of a different solution, this one involves a stack. If you have never heard about a "stack" I highly recommend you to read my ["Stacks and Queues a Beginners Overview"](https://blog.garybricks.com/stacks-and-queues-a-beginners-overview) post and come back here.

We can iterate the array backward from right to left, and for each element perform the following algorithm:

1.  If our helper stack is empty, output -1, add the element to the stack, and continue to the next element.
    
2.  else, check the element that is on the top of the stack, and if it's smaller than the current element, output the top of the stack and add the current element to the stack, don't delete the top!
    
3.  if the top of the stack is not smaller, remove the top of the stack until either steps 1 or 2 are fulfilled.
    

### Algorithm Visualization

If you are struggling to understand this solution, check out the animation below of the algorithm in action with the first input example.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1671131655858/1SkPALivF.gif align="center")

### Code Implementation

I highly encourage you to code the algorithm as described above in the language of your choice. here is my implementation in c++:

```cpp
#include <iostream>
#include <vector>
#include <stack>
#include <algorithm>
using namespace std;

int main(){
	int n; cin >> n;
	vector<int>arr(n); for(auto &e:arr)cin >> e;
	stack<int>S;
	vector<int>result;
	for(int i=n-1; i>=0; i--){
		while(true){
			if(S.size() == 0){result.push_back(-1); S.push(arr[i]); break;}
			if(S.top() < arr[i]){
				result.push_back(S.top());
				S.push(arr[i]);
				break;
			}else{
				S.pop();
			}
		}
	}
	reverse(result.begin(), result.end());
	for(auto &e:result)cout << e << " ";
	return 0;
}
```

### Time and Space Complexity

The efficiency of this algorithm depends on the total number of stack operations. if the current item is larger than the top element of the stack it gets directly added to the stack in constant time ***O(1)***. However, if it's not, we might have to remove several elements of the stack which has a worst-case of ***O(N)***, this might look like it can have a total worst-case complexity of ***O(N^2)*** but in reality, each item in the array is going to be added exactly once and removed at most one time. Thus, the time complexity of this program is going to be: ***O(N)***.

## Problem Variations

Up until this moment, the problem consists of finding the minimum nearest element to the right, however, you can also find the Maximum item by just changing a single character. before: `if(S.top() < arr[i])` After: `if(S.top() > arr[i])`. Another common variation is to find the minimum nearest element to the **left**. To do that simply iterate the array normally from left to right and don't reverse the `result` array.

```cpp

int main(){
	int n; cin >> n;
	vector<int>arr(n); for(auto &e:arr)cin >> e;
	stack<int>S;
	vector<int>result;
	for(int i=0; i<n; i++){
		while(true){
			if(S.size() == 0){result.push_back(-1); S.push(arr[i]); break;}
			if(S.top() < arr[i]){
				result.push_back(S.top());
				S.push(arr[i]);
				break;
			}else{
				S.pop();
			}
		}
	}
	for(auto &e:result)cout << e << " ";
	return 0;
}
```

## Conclusion - Farewell

You've reached the end of this post, hope you enjoyed the solution for this classical competitive programming problem and learned something new. Here are some related posts:

*   [https://blog.garybricks.com/stacks-and-queues-a-beginners-overview](https://blog.garybricks.com/stacks-and-queues-a-beginners-overview)
    
*   [https://blog.garybricks.com/efficiency-and-big-o-notation-overview-with-python-examples](https://blog.garybricks.com/efficiency-and-big-o-notation-overview-with-python-examples)
    
*   [https://blog.garybricks.com/programmers-guide-to-solving-computational-problems](https://blog.garybricks.com/programmers-guide-to-solving-computational-problems)
    

Let me know in the comments what you thought about this post and let me know what you will like to see next. See you in the next post, stay tuned!