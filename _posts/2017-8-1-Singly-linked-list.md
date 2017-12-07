---
layout: post
title: Singly Linked list implementation in Python
---

In computer science, a linked list is a linear collection of data elements, in which linear order is not given by their physical placement in memory. Each pointing to next node by means of a pointer. It is a data structure consisting of a group of nodes which together represent a sequence. Under the simplest form, each node is composed of data and a reference (in other words, a link) to the next node in the sequence. This structure allows for efficient insertion or removal of elements from any position in the sequence during iteration.(Source: https://en.wikipedia.org/wiki/Linked_list)

Today I will explain how to implement a “Singly linked list” in Python, which will contain functions to insert , delete and search any item in the linked list and functions to get the size and print the whole linked list. So, first of all we should know what is a singly linked list ?

Singly linked list: Singly linked lists contain nodes which have a data field as well as a 'next' field, which points to the next node in line of nodes. Operations that can be performed on singly linked lists include insertion, deletion and traversal.

<img src= "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Singly-linked-list.svg/408px-Singly-linked-list.svg.png">

<h6>(A singly linked list whose nodes contain two fields: an integer value and a link to the next node, Source:https://en.wikipedia.org/wiki/Linked_list )</h6>


Let’s get started!

First , we will create a class named "Node" which will contain a data and a pointer (which is here as next_node) to the next node. Initially we will set the data and next_node(pointer) equal to None so that if we don’t send any data and pointer to the next node, it will return None.

Then create two methods named "get_data" and "get_next" and will return the data and the next node respectively.
We will add another method "set_next" which will take a new node as a parameter and will set the pointer from previous node towards this node.


```python
class Node:
    
    def __init__(self,data=None,next_node=None):
        self.data = data
        self.next_node = next_node
    
    def get_data(self):
        return self.data
    
    def get_next(self):
        return self.next_node
    
    def set_next(self,new_node):
        self.next_node = new_node
```


Now, create a class Linked_list and set the head of the list to None in the __init__ method.


```python
class Linked_list:
    
    def __init__(self,head=None):
        self.head = head
```


Add a method "insert_head" , first it will take a data  and create a Node by it and set it to the variable new_node. Then set the pointer of this node towards the next node by sending self.head as parameter. As at the beginning the head is None so the pointer will be set to the None. Now, we will set the node we created as head. So, what does this method do ? The method take data and insert is as head in the linked list. 


```python
def insert_head(self,data):
    new_node = Node(data)
    new_node.set_next(self.head)
    self.head = new_node
```


A question can come across your mind, can I insert data as tail ? The answer is yes ,so let’s see how to do it!

This "insert_tail" method take a data and make a node from it and set it to the variable. Now , two things to be considered. What to do if the list is empty ? Or the list is not empty ? So at first we check if head is None and if it is then we are assured that list is empty and we set the node as head(because there must be an element to add another element as tail). But if head is not None then the list isn’t empty and we traverse the list using the get_next method to go to the end of it. When we find that pointer of the previous node is null, we set the pointer towards the node we created. Yeah! we have inserted an element in the list as tail.


```python
def insert_tail(self,data):
    new_node = Node(data)
    current = self.head
    if current is None:
        self.head = new_node
    else:
        while current.get_next():
            current = current.get_next()
        current.set_next(new_node)
```


To delete an element from the linked list create a method named "delete" which takes a data you want to delete as a parameter. Set head to the variable current and create variable prev which will store the previous element , initially it is equal to None. Now, we traverse through the list to check whether it contains our data or not, if the data is in any Node then we check if there is any previous Node of the Node that contains our data. If there is any previous Node then we set the pointer of the previous Node to the next Node of our data. If there is no previous Node that means our data is the head so we set the next element as head. If we don’t find the data then we go to the next Node by setting current Node to prev variable and next Node of the current Node to current variable
 
 
```python
def delete(self,data):
    current = self.head
    prev = None
    while current:
        if current.get_data() == data:
            if prev:
                prev.set_next(current.get_next())
            else:
                self.head = current.get_next()
            break
        else:
            prev = current
            current = current.get_next()
```


To check whether an element is in the linked list or not ,create a method named "search" which takes a data that we want check if it is in the linked list. First , we set the head to the current variable and we iterate through the list while current is not None and if we get the data in the list we return True  and if we don’t we go to next Node. If we don’t find the data and current is None then we return False. 


```python
def search(self,data):
    current = self.head
    while current:
        if current.get_data() == data:
            return True
        else:
            current = current.get_next()
    return False
```


To know the size of the linked list, we are going to use dunder/magic method __len__ . Because of using this dunder method we can get the size using len(). This makes our work easier and readable.


```python
 def __len__(self):
    return len(self.temp)
```


At last we want to print the linked list as a list we usually see.
So, create a method "print_list", declare a variable to store the head
and another variable temp which initially stores an empty list. Now we traverse through the linked list while current is not None  and we append every element in the temp list till current is None then we print the list.


```python
def print_list(self):
    current = self.head
    self.temp = []
    while current:
        self.temp.append(current.get_data())
        current = current.get_next()
    print(self.temp) 
```


Now it’s time to check out the linked list we have written,


```python
item1 = 1020
item2 = 2040
item3 = 3060
item4 = 4080
 
li = Linked_list()

li.insert_head(item1)
li.insert_head(item2)
li.insert_head(item3)
li.insert_head(item4)

li.print_list()
>>> [4080, 3060, 2040, 1020]

print(li.search(3060))
>>> True
print(li.search(9010))
>>> False

li.delete(2040)
li.print_list()
>>> [4080, 3060, 1020]

print(len(li))
>>> 3 

li.insert_tail(50100)
li.print_list()
>>> [4080, 3060, 1020, 50100]
```

It works! 

Feel free to ask any question and comment for any kind of correction.


