---
title: "A Beginners Overview of Linked Lists in Python"
seoTitle: "A Beginners Overview of Linked Lists in Python"
seoDescription: "In this post, we will cover what are linked lists? what are they for? pros and cons? types of linked lists and the most common methods to interact with them"
datePublished: Tue Dec 07 2021 19:09:43 GMT+0000 (Coordinated Universal Time)
cuid: ckwwh8i4r07h5pqs1dymla827
slug: a-beginners-overview-of-linked-lists-in-python
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1637607859343/44ZQ7xDEH.jpeg
tags: algorithms, data-structures, python3, beginners, competitive-programming

---

## Introduction
Hello everyone, welcome back!, today I wanted to give a beginners overview of Linked Lists, we will take a good look at what are they? what are they for? and we will look through some examples together.

## What is a Linked List?
A linked list is an extension of a list but it's definitely NOT an array. By definition a linked list is a:

> Dynamic data structure where each element (called a node) is made up of two items: the data and a reference (or pointer), which points to the next node. A linked list is a collection of nodes where each node is connected to the next node through a pointer.

Here it's an image to give a better understanding of a linked list

![linked_vs_array.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1637603328903/E1PjE0gz9.jpeg)

With a linked list, there are still some things that have order but there are no indices. Instead, a linked list is characterized by its `Links`. Each element has a notion of what the next element is since it's connected to it, but not necessarily how long the list is or where it is in the list.
An array's different. There is nothing in one element of the array that says "here's your next element" like a linked list would, instead an array knows what the next element is by what the next `index` is.

## Differences between an array and a linked list
Let's walk through the differences together.

### Array
- A data structure consisting of a collection of elements each identified by the array index.
- Supports random access, the programmer can directly access an element in the array using an index
- Elements are stored in contiguous memory locations
- Programmer has to specify the size of the array when declaring the array
- Elements are independent of each other

### Linked list

- A linear collection of data elements whose order is not given by their location in memory. 
- Supports sequential access, the programmer has to go sequentially through each element until reaching the searched element
- Elements can be stored anywhere in memory
- There is no need in specifying the length of the linked list
- An element has to point to the next or previous element

When talking about linked lists you will often hear "Node" instead of "Element"

## Why linked lists?
When I was studying linked lists I was already pretty familiar with arrays and felt pretty comfortable using them, and if you are a beginner you are probably feeling the same way and are wondering "Hey, arrays are easy to access, have a set length, the elements are independent of each other, why make my life harder with this new linked list stuff?", if you thought of that, congratulations! you are on your way to becoming a great programmer since you have to always ask yourself the why of things.

The answer to the question "Why use linked lists?" can be a complex one, but for now, the simple and short answer is Efficiency. Turns out, that adding or removing an element from a linked list is so much easier in comparison to an array. And I want to give a quick reminder that we are working with python here.

## Implementing a Linked List
Let's learn more about linked lists while we work through some examples and start writing some code.

![implementing_basic_linked_list.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1637692001097/BF--Qq4bQ.jpeg)

Because of the definition we saw earlier, we are going to approach this, by creating a `Node`, a node it's going to have, two attributes, the value, and the `next` attribute that's going to be a pointer pointing to the next node. From the image above, we can see how each node points to the next one until the list it's finished and the last node points to `None`. this collection of nodes pointing to the next one is going to be the Linked List.

### Step - 1 Create a Node class with value and next attributes
```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
```
this node has a "value" property that can be passed as an argument, and a "next" attribute that points to the next `Node`, in this case, it's pointing to None by default.

### Step - 2 Creating a Head Node
Using our newly created Node class, it's time to create our `Head`, the "Head" it's basically the first Node.
```python
head = Node(8)
```
Creating a new Node with the value of 8 and saving it in a new head variable.

### Step - 3 Creating Second Node and Linking it
Like we saw in the previous step, to create a new Node simply code `Node(value)`, and to link it to the head what we need to code is:
```python
head.next = Node(4)
```
In the code above, `head.next` had the value of None, but now we are replacing that with a new Node with the value of 4.

### Step - 4 Printing Out The Values
Right now, we have a linked list that has a Head with the value of 8 then the next node with the value of 4 like this:

![linked_list_progress1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1637694869025/9bhT0bd7B.png)

Here's our progress:
```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None
        
head = Node(2)
head.next = Node(1)
```
To print out the values in the linked list we have to code:
```python
print(head.value)
print(head.next.value)
```

```
Output:
8
4
```

### Step - 5 Extending our linked list
Let's remember that this is what we want to accomplish:

![current_vs_goal.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1637697908154/Xo8-HkIR4.jpeg)

To do this, we need to create three more nodes, and we need to attach each one to the next attribute of the node that comes before it. Notice that we don't have a direct reference to any of the nodes other than the head.
```python
head.next.next = Node(2)
head.next.next.next = Node(5)
```
Let's print all the values:
```python
print(head.value)
print(head.next.value)
print(head.next.next.value)
print(head.next.next.next.value)
```

### Step - 6 Traversing List
This process isn't very efficient, let's write a function that receives the head and traverses the linked list to print out all of the values.
```python
def print_linked(head):
    current = head  # current node set to the head
    while current: # loop that will run as long as current exists
        print(current.value) # printing the current node value
        current = current.next # moving to the next node

print_linked(head)

```
Ahh, so much better, now, no matter how long the linked list is, with `print_linked(head)` we no longer need to code `print(head.next.next.next.next)` you get the point.

### Step - 7 Creating Linked_List class
Up until now, we have to create a variable with the head and pass that to our functions in order to interact with it, but an alternative it's to create a Linked_List class and code methods to it. Let's take a look at some code to understand what I mean.
```python
# Linked_List class with a default head value of None meaning empty list
class Linked_List:
    def __init__(self):
        self.head = None
```
Let's add our print function as a method to this class.
```python
    def print_linked(self):
        current = self.head
        while current:
            print(current.value)
            current = current.next
```
In the code above, we made tiny changes to fit in as a method, in this case instead of receiving the head, we receive the `self` attribute, and instead of setting current to the head, we set it to the `self.head`, other than that, everything stays the same.

Now, we have our Linked list class with a print method and we have to create the actual object like this:
```python
my_linked_list = Linked_List()
```
and if we wanted to print the values of that linked list, all we have to do is:
```python
my_linked_list.print_linked()
```

If you tested the lines above you should have seen no output since the linked list is completely empty, let's change that by adding a method that allows us to append items into the list.

```python
    def append(self, value):

        # checking if the linked list is empty
        if self.head is None:
            # If so, set the head to a new node with the passed value
            self.head = Node(value)
            return
        
        # Traverse the linked list until reaching the end of the list
        current = self.head
        while current.next:
            current = current.next

        # Append the new node with the passed value
        current.next = Node(value)
```

Here's the full code:
```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None


class Linked_List:
    def __init__(self):
        self.head = None

    def print_linked(self):
        current = self.head
        while current:
            print(current.value)
            current = current.next

    def append(self, value):
        if self.head is None:
            self.head = Node(value)
            return

        current = self.head
        while current.next:
            current = current.next

        current.next = Node(value)


my_linked_list = Linked_List()  # this is creating a Linked_List object
my_linked_list.append(8)  # appending 8 to the list
my_linked_list.append(4)  # appending 4 to the list
my_linked_list.append(2)  # appending 2 to the list
my_linked_list.append(5)  # appending 5 to the list
my_linked_list.print_linked()  # printing the list
```

If you test the code above you shall now see an output of `8 4 2 5` like the image below

![result_list.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638213481627/xigRLdw9l.png)

## Adding more methods
I hope you're getting the hang of this, let's try adding more methods that will make working with linked lists better.

Below you will find the exercises for this section, I highly encourage you to try to code them yourself before watching the solutions that can be found at the end of this section. And I also recommend you try each of the methods individually first before trying to use multiple of them together.

### Add a `to_list()` method
When the method is called on the linked list it should convert the linked list back into a normal python list.
```
output: 
[8,4,2,5]
```

### Add a `prepend()` method
Method similar to the `append()` method but instead of appending at the end of the linked list it will append at the beginning of the list
```python
my_linked_list.prepend(7)
my_linked_list.print_linked()
```
```
output: 
7
8
4
2
5
```

### Add a `search()` method
`print(my_linked_list.search(4))` will return the Node if there is one with a matching value, if not, it will return a ValueError indicating that the searched value is not found in the list. Because it returns the searched Node you can access its value like this:

```python
# if there is a node with the value of 4, 4 will be printed
print(my_linked_list.search(4).value) 
```
```
output: 
4
```

### Add a `remove()` method
Method traverses the linked list and removes the Node with the passed value
```python
my_linked_list.remove(4)
my_linked_list.print_linked()
```
```
output: 
7
8
2
5
```

### Add a `pop()` method
Method that removes the first node of the linked list
```python
my_linked_list.pop()
my_linked_list.print_linked()
```
```
output: 
8
2
5
```
### Add a `insert()` method
This method receives a position and a value and inserts a new node with the passed value in the passed position
```python
my_linked_list.insert(10,1)
my_linked_list.print_linked()
```
```
output: 
8
10
2
5
```

### Add a `size()` method
This method shall return the length of the linked list like the method `len()` would on a normal python list
```python
print(my_linked_list.size())
```
```
output: 
4
```

### Add a `reverse()` method
Reversing a linked list is a really common interview problem and I highly recommend that you put extra effort into understanding this method. This method shall, like the name suggests, reverse the linked list nodes order.
```python
my_linked_list.reverse()
my_linked_list.print_linked()
```
```
output: 
5
2
10
8
```

## Full Code

Feel free to test out combinations of the methods and try each one individually and do your best in understanding them. You can also try adding your own methods, and remember that the solutions shown below are not the only correct ways of coding them.

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None


class Linked_List:

    def __init__(self):
        self.head = None

    # ------------------------------------------ #

    def print_linked(self):
        current = self.head
        while current:
            print(current.value)
            current = current.next

    # ------------------------------------------ #

    def append(self, value):
        if self.head is None:
            self.head = Node(value)
            return

        current = self.head
        while current.next:
            current = current.next

        current.next = Node(value)

    # ------------------------------------------ #

    def to_list(self):
        out = []
        node = self.head
        while node:
            out.append(node.value)
            node = node.next
        return out

    # ------------------------------------------ #

    def prepend(self, value):
        if self.head is None:
            self.head = Node(value)
            return

        new_head = Node(value)
        new_head.next = self.head
        self.head = new_head

    # ------------------------------------------ #

    def search(self, value):
        if self.head is None:
            return None

        node = self.head
        while node:
            if node.value == value:
                return node
            node = node.next

        raise ValueError("Value not found in the list.")

    # ------------------------------------------ #

    def remove(self, value):
        if self.head is None:
            return

        if self.head.value == value:
            self.head = self.head.next
            return

        node = self.head
        while node.next:
            if node.next.value == value:
                node.next = node.next.next
                return
            node = node.next

        raise ValueError("Value not found in the list.")

    # ------------------------------------------ #

    def pop(self):
        if self.head is None:
            return None

        node = self.head
        self.head = self.head.next

        return node.value

    # ------------------------------------------ #

    def insert(self, value, pos):
        if self.head is None:
            self.head = Node(value)
            return

        if pos == 0:
            self.prepend(value)
            return

        index = 0
        node = self.head
        while node.next and index <= pos:
            if (pos - 1) == index:
                new_node = Node(value)
                new_node.next = node.next
                node.next = new_node
                return

            index += 1
            node = node.next
        else:
            self.append(value)

    # ------------------------------------------ #

    def size(self):
        size = 0
        node = self.head
        while node:
            size += 1
            node = node.next

        return size

    # ------------------------------------------ #

    def reverse(self):
        previous = None
        current = self.head
        while current:
            next = current.next
            current.next = previous
            previous = current
            current = next
        self.head = previous

    # ------------------------------------------ #


my_linked_list = Linked_List()  # creating linked list obj

my_linked_list.append(8)  # appending 8
my_linked_list.append(4)  # appending 4
my_linked_list.append(2)  # appending 2
my_linked_list.append(5)  # appending 5
my_linked_list.print_linked()  # output: 8 4 2 5

print(my_linked_list.to_list())  # output: [8,4,2,5]

my_linked_list.prepend(7)  # appending 7 to the start of the linked list
my_linked_list.print_linked()  # output: 7 8 4 2 5

print(my_linked_list.search(4).value)  # output: 4

my_linked_list.remove(4)  # remove the node with value 4 from the list
my_linked_list.print_linked()  # output: 7 8 2 5

my_linked_list.pop()  # remove the first node
my_linked_list.print_linked()  # output: 8 2 5

my_linked_list.insert(10, 1)  # insert node with value 10 in position 1
my_linked_list.print_linked()  # output: 8 10 2 5

print(my_linked_list.size())  # output: 4

my_linked_list.reverse()  # reverse the order of the nodes
my_linked_list.print_linked()  # output: 5 2 10 8

```

## Types of Linked Lists
### Singly Linked List
Up until this point, we have been working with a type of linked list called: "singly linked list", in this kind of linked list, each node is connected only to the next node in the list.

![result_list.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638307507807/g1QmuRVfF.png)

This connection is typically implemented by setting the `next` attribute on a node object itself. But there are more types of linked lists.
 
### Doubly Linked List
This type of list is the exact same as the singly linked list with the addition of also having a connection backward.

![Doubly linked list.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638388293420/YLFN0ZQP8.png)

To implement a Doubly linked list simply change your node to have a previous property like this:
```python
class DoubleNode:
    def __init__(self, value):
        self.value = value
        self.next = None
        self.previous = None # new property
```

#### Why use Doubly linked lists?
using doubly linked lists can give us advantages that a singly linked list can't, for example, now that we track the tail, we can do things like appending a node to a list's tail in constant time.
```python
def append(self, value):
    if self.head is None:
        self.head = DoubleNode(value)
        self.tail = self.head
        return

    self.tail.next = DoubleNode(value)
    self.tail.next.previous = self.tail
    self.tail = self.tail.next
    return
```

### Circular Linked Lists
Linked circular lists occur when the chain of nodes links to itself somewhere. For example, NodeA -> NodeB -> NodeC -> NodeD -> NodeB is a circular list because NodeD points to NodeB creating a NodeB -> NodeC -> NodeD -> NodeB loop.

![circular linked list.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638411442140/yPlrkcgfI.png)

A circular linked list in simple words, it's a singly or doubly list where all nodes are connected to form a loop or "circle" meaning there is no NULL at the end, this can be a problem since if we try to iterate through it we will never find the end. We usually want to detect if there's a loop in our linked list to avoid an infinite iteration.

## Detecting Loops in Linked Lists
 In this section, we'll see a way we can detect loops in a linked list with python. The way we'll do this is by using two pointers called "runners", both of them will traverse through the linked list but one of them it's going to iterate twice as fast, meaning it will advance two nodes at a time.
If a loop exists, the fast runner will eventually catch up with the slow runner and both pointers will be pointing at the same node at the same time, if this happens you will know for sure there's a loop, see the image below to understand this technique.


![linked List Loop Detection.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1638588946123/wkoDuzPwP.gif)

![loop in linked list.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638414846551/K9WLgxaHV.png)

### Exercise - 9 Add a `hasLoop()` method
I'm confident you can do this on your own, see the image above thoroughly to understand the algorithm you're about to code, and also take another look at the past exercises, you should find everything you need in this post. Make your best effort! and don't worry if you don't get it right away we'll see the solution below.

### Solution `hasLoop()` method
The first thing we need to do is to define our `hasLoop()` method:
```python
def hasLoop(self):
    # your code goes here
```
Next, we'll check if the list is empty, in the case that the condition is True we'll return False meaning there is no loop
```python
    if self.head is None:
        return False
```
Then, we need to create our two pointers as we talked about earlier
```python
    slow = self.head
    fast = self.head
```
Now the fun part! while the fast node and the fast.next node exists, let's advance the slow node by one and the fast by two
```python
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
```
and for each iteration, we need to check if the slow node is the same as the fast one, if that is the case then we just found a loop and the code should return True, if the while loops finishes, it means there was an end to the list and the code should return False.
```python
        if slow == fast:
        return True
    return False
```

Full code:

```python
    def hasLoop(self):
        if self.head is None: # check if the linked list is empty
            return False # return False, meaning there is no loop

        slow = self.head # create the slow node
        fast = self.head # create the fast node

        while fast and fast.next: # while fast and fast.next exist:
            slow = slow.next # advance the slow node by one
            fast = fast.next.next # advance the fast node by two

            if slow == fast: # if the nodes are the same
                return True # return True, meaning there is a loop

        # if the loop finishes, that means there was an end to the list
        # and there was no loop
        return False
```

## Flatten a Nested Linked List
Let's suppose we have a **nested** linked list, this means that the value of each node in the linked list is another ordered linked list. The image below illustrates this.

![oredered nested linked list.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638497197984/dFk0NBTts.png)

In this section, we'll **flatten** this linked list, which means to combine all nested lists into one **ordered** single linked list like this:

![goal nested linked list.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638497146402/P8U_ysIIR.png)

### Step - 1 Define a `NestedLinkedList` class
This class should inherit the Linked_List class and inside of the new class let's add our flatten method.
```python
class NestedLinkedList(Linked_List):
    def flatten(self):
        # code goes here
```

### Step - 2 Define a `merge()` Helper Function
This function will be useful for merging two linked lists and having them into a single **ordered** linked list, this function it's not going to be a `NestedLinkedList` method and should return an instance of LinkedList.

```python
def merge(list1, list2):
    # your code goes here
    return
```

### `merge()` walkthrough
Note, this solution expects the passed lists to be ordered.

First, we need to create a new LinkedList object, that will be named `merged`
```python
    merged = Linked_List()
```
Next, let's check whether any of the passed lists are None. If list1 is None, immediately return list2, if list2 is None, immediately return list1.

```python
    if list1 is None:
        return list2
    if list2 is None:
        return list1
```

Then, we'll create two traversers, one called list1_node and the second one called list2_node. And using both of them, we'll traverse both lists while they exist.
```python
    list1_node = list1.head
    list2_node = list2.head
    while list1_node or list2_node: # pay attention to the OR
```
If the first node does not exist, meaning the first list is traversed, append the list2_node to the "result list"(merged) and advance the list2_node to the next node in that list.
```python
        if list1_node is None: # if list1 is traversed
            merged.append(list2_node.value) # append the second list node to the "result"
            list2_node = list2_node.next # and advance the second node to the next one
```
Repeat the step above but with the list2
```python
        elif list2_node is None: # if list2 is traversed
            merged.append(list1_node.value) # append the first node to the "result"
            list1_node = list1_node.next # advance the first node to the next one
```
Now we can work in the cases that none of the lists are done traversing. Which would always be the first iteration.

Because we want the output to be an <mark>ordered</mark> linked list but with both lists merged, we need to check which node has the smallest value and append it.
```python
        # if the first node value is smaller than the second node value
        elif list1_node.value <= list2_node.value:
            merged.append(list1_node.value) # append the first node
            list1_node = list1_node.next # and advance to the next node
        else: 
            merged.append(list2_node.value) # append the second node
            list2_node = list2_node.next # advance to the next node
```

Finally, after the while loop exits indicating that both lists have been traversed, return the result, (merge) linked list.
```python
    return merged
```
Here's the full `merge()` procedure:
```python
def merge(list1, list2):

    merged = Linked_List()

    if list1 is None:
        return list2
    if list2 is None:
        return list1

    list1_node = list1.head  # [5,6,7] list one
    list2_node = list2.head  # [1,2,3] list two
    while list1_node or list2_node:  # 5 - 1
        if list1_node is None:  # if list1 is traversed
            # append the second list node to the "result"
            merged.append(list2_node.value)
            list2_node = list2_node.next  # and advance the second node to the next one
        elif list2_node is None:  # if list2 is traversed
            # append the first node to the "result"
            merged.append(list1_node.value)
            list1_node = list1_node.next  # advance the first node to the next one
        # if the first node value is smaller than the second node value
        elif list1_node.value <= list2_node.value:
            merged.append(list1_node.value)  # append the first node
            list1_node = list1_node.next  # and advance to the next node
        else:
            merged.append(list2_node.value)  # append the second node
            list2_node = list2_node.next  # advance to the next node
    return merged

```

### Finishing `Flatten()` Method
With the help of our `merge()` helper function, there is an easy solution to finish our `Flatten()` method by using **recursion**.

We won't talk about recursion in detail in this post, but for those that are not familiar with the concept, recursion is basically invoking a function inside itself, here's a code example that returns the factorial of any number.

```python
def factorial(x): # function definition
    if x == 1: # break point, important to exit the "loop"
        return 1
    else:
        return (x*factorial(x-1)) # invoking itself


print(factorial(4))  # 4 * 3 * 2 * 1 = 24
```

As you can see from the code above, the `factorial()` function it's being invoked inside of itself, that's a recursive function.

Back to our `Flatten()` method. Let's apply recursion!
```python
class NestedLinkedList(Linked_List):
    def flatten(self):
        return self._flatten(self.head)

    def _flatten(self, node):  # a recursive function

        # A termination condition
        if node.next is None:
            # if there is no next node in the list
            # merge the last, current node
            return merge(node.value, None)

        # _flatten() is calling itself untill a termination condition is achieved
        # <-- Both arguments are a simple LinkedList each
        return merge(node.value, self._flatten(node.next))
```

### Testing `flatten()` Function
First, let's create three simple, normal,ordered, linked lists.
```python
''' Create a simple LinkedList'''
linked_list = Linked_List()
linked_list.append(0)
linked_list.append(4)
linked_list.append(8)
linked_list.print_linked()
# 0 => 4 => 8

''' Create another simple LinkedList'''
second_linked_list = Linked_List()
second_linked_list.append(1)
second_linked_list.append(2)
second_linked_list.append(3)
second_linked_list.print_linked()
# 1 => 2 => 3

''' Create another simple LinkedList'''
third_linked_list = Linked_List()
third_linked_list.append(6)
third_linked_list.append(7)
third_linked_list.append(9)
third_linked_list.print_linked()
# 6 => 7 => 9
```
Next, let's create a **nested** linked list object using our class
```python
nested_linked_list = NestedLinkedList()
```
Something really cool, it's that when we defined the `NestedLinkedList`class, we <mark>inherited</mark> the `Linked_List` class, which means that all of the previous methods we wrote for the `Linked_list` class are going to be available to use in the `NestedLinkedList` class.
```python
# Here we inherited the Linked_List class
class NestedLinkedList(Linked_List):  # making all of its methods available here too!
```

Now, let's append the three simple linked lists into this `nested_linked_list` using the `append()` method.

```python
nested_linked_list.append(linked_list)
nested_linked_list.append(second_linked_list)
nested_linked_list.append(third_linked_list)
```
Lastly, create the flattened list like this:
```python
flattened = nested_linked_list.flatten()
```
and print it out!
```python
flattened.print_linked()
```

## Conclusion - Farewell
You've reached the end of this lesson on Linked Lists, we saw what are they? how do they differentiate from a normal python list? what are some pros and cons? and we also saw code examples of the most common ways to interact with Linked lists.

I really hope some of the guidelines we saw today were helpful and the basic foundations on this topic were well understood, remember, there is still a lot to learn and we definitively didn't cover everything on linked lists, but I hope this was a good beginner overview and that you grasped the concepts and feel more confident on your programming journey.

Let me know in the comments what you thought about this post and let me know what you will like to see next. See you in the next post, stay tuned!

