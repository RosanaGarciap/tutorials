
Tutor: Rosana Garcia

# Welcome Message

<font size="4">Hi dear reader, and welcome to Introduction to Data Structures! </font>

Thanks for your interest in our **Data Structures Tutorial**, in this course you will find easy explinations for three of the most used data structures: Linked List, Queue, and Trees. Be aware that our course will not contain all types of modern functionalities and representations of these structures, the goal is help you to obtain the basic knowledge required for you to understand how data structures work, and how they can be applied to model real life events.

# Introduction to Data Structures Concepts

## What is a Data Structure? 🧱

The first concept you need to understand is the concept of Data Structure, the definition can be easily guessed by the words that compose it Data and Structure.

A Data is a value. Yes, as simple as it sounds, data are just values that have not meaning by themself. Think of a data as a brick of Legos, if you have a bunch of Lego's bricks they can't really do or mean anything unless you give it to them. In programming, data values can be classified according to it's type (block colors), it can be a basic type such as Integer, Float, and Char or more complex types like String and Null.

Data by itself has no special meaning just like a brick doesn't look special by itself, however, when provided data is grouped following a pattern it can be used to represent different elements of life. As when you unite blocks to built a castle or an car, if you have the number **2** it says nothing to you, but if you have the expression **2+2=4** Now that you understand that the sum of 2 with itself is equals to 4, even more, with more data of the same kind we can infere the sum of any numeric value with itself is equals to two times its original value.

Now that you understand what is Data pounder about the next question. What kind of information can I get if instead of a data alone I have a set of diferent kinds of datas organized in such a way that every data represents something in specific, and that's were the word structure take place.

<div style="display:flex;" >
<img src="./legos1.jpg"/>
<img src="./legos2.jpg"/>
</div>

A data structure is a set of data elements organized following a formal logical model for an abstract representation of something, like the car made of legos it is not a real car but an abstract representation of it. That means the data can organized together as a whole and this whole is built specifically to simulate the behavior or characteristic of something on the real world. The type of datas that will be used, it's organization, along with the operations or functionalities that can be applied over them, facilitate the effective use and manipulation of information.

### Common Data Structures

In the progrmming world, exist a set of data structures which attributes and the operations that can be made over them are already defined at international level. In this course we will study 3 of them:

1. Linked List
2. Queue
3. Tree

# Linked Lists ⛓

 [*"A linkeed List is a linear data structure, in which the elements are not stored at contiguous memory locations. The elements in a linked list are linked using pointer."*](https://www.geeksforgeeks.org/data-structures/linked-list/) 

If you have an list of students, let's call this list *names*, this list contains three names, *Juan, Jane*, and *Peter* in that order. To create this list you may think in create an array of strings, in such case if you want to access the value *Peter*, you just need to use indexing like names[3] or name[2] depending if the array index starts with the position 1 or 0, in our case the values will start with 1. However, since arrays have limited memory space soon or latter you will face an overflow issue when you reach the limit, that's where the concept of Linked List appears. A linked list creates the ilussion that values are storage in sequential order like arrays, however, that's not the case.

## Pointer
<hr>

To understand Linked List completely we need first get aquantiance with the concepts of pointers and node.

In programming, a pointer is a variable that storage the memory address of another variable. Pointers is always a new and difficult topic for begginners, but it will be understanble with the following example.

In the next image the names between brackets represent a list (please don't confuse it with an array). We have our memory and it has blocks where we can store data, we are going to represent symbolically the addresses of such blocks with integers. As you can see, the values are storaged in different places and are not really in order, to keep track of where these values are, and their order we need to use pointers.

<img src="./memory-addresses.jpg"/>

Something interesting is that users don't really have control of how the computer references or assign this memory address values. As you can see in the next figure the values of the index in high programming level (1, 2, and 3) is not the same as in the low computer level.

<img src="./array-pointer.jpg"/>
<br>

To resume, pointers don't store the literal values you want to use, they are references to the place where where the value are located.
<br>

## Node 🧩
<hr>

In the last example we could see that we make use of pointers to get the memory addresses where the values of our linked lists are storaged, but how this is trully accomplished? the answer is **'Nodes'**.

A Node [*"is a basic data structure that contains data of any type and one or more pointers to other nodes"*](https://www.codecademy.com/learn/linear-data-structures/modules/cspath-nodes/cheatsheet#:~:text=A%20Node%20is%20a%20data,link%20to%20the%20next%20node.) 

Before we compared data in general as Lego's blocks, however, the Nodes are more like puzzle pieces. When you solve a puzzle you need that every piece can be related to other specific puzzle pieces to ensure that the order will be kept and the puzzle can be solved. In a similar way sequential elements like Liked Lists require that each element can keep a register of who comes after them and sometimes who they have before.

<div style="display: flex">
<img src="./puzzles.jpg"/>
<img src="./linkedList.jpg"/>
</div>
<br>


## **LinkedList implementation with Python Code**

### Attributes
Each Node has:
1. Data (Object) to storage
2. Pointer to the next node
3. Pointer to the previous node (Double Linked List)

Linked List has:
1. size : INTEGER            -> The lenght of the list
2. head : NODE               -> Node that points to the first Node of the list
3. Tail : NODE               -> Node that points to the last Node of the list

```
class LinkedList:
    """
    Nested class Node:  instance of the Node class that will be stored 
    into de Linked List
    """
    # Node Class Constructor
    class Node:
        """
        Node class constructor, create an instance of the Node class that will be stored 
        into de Linked List
        """
        def __init__(self,value):
            self.value = value
            self.next = None
            self.prev = None
    """
    Linked List class constructor, initialize an empty Linked List
    """            
    def __init__(self):
        self.__size = 0
        self.head = None
        self.tail = None

```
## Linked List Functions

1. insert() -> add an new element (Node) at the end of the list

```
    def insert(self, value):

        # Verify first if the List is empty
        #   If is not empty walk through each node until you find the last node  (´next´ value equals to null pointer)
        #   in other case, initialize the head of the List

        if(self.head!=None):
            current = self.head
            aux = self.head.next
            stop = False
            while (not stop ):
                if(aux==None):
                    # create new node
                    current.next = LinkedList.Node(value)
                    # make the tail point to the new node
                    self.tail = current.next
                    self.tail.prev = current
                    stop = True
                else:
                    current = aux
                    aux = current.next
        else:
            self.head = LinkedList.Node(value)
            self.tail = self.head
        self.__size = self.__size+1
```

2. remove() -> remove the last element (Node) of the list and update the tail.

```
    def remove(self):
        # Verify first if the List is empty

        # If is not empty walk through each node until find the last node  
        # (´next´ value equals to null pointer) and remove it from the list
        if (self.__size > 0):
            if(self.tail!=None):
                if(self.__size > 1):
                    current = self.tail.prev
                    current.next = None
                    self.tail = current
                elif(self.__size == 1):
                    self.head.next == None
                    self.tail == self.head
                else:
                    self.head == None
                    self.tail == None
            self.__size = self.__size-1
        else:
            print("Error >> Current list is empty!")
```

3. size() -> returns the lenght of the linkedList

```
    def size(self):
        return self.__size
```
## Student's name returns the lenght of the linkedList

```
    def size(self):
        return self.__size
```

## Homework

Write in python a "search" function that given a value return the first position (index) where it's found in the linked list. In case the value is not in the list return None. (suppose the index starts from 0).

<details>
  <summary>**Answer: Don´t see it until you finish your own code**</summary>
  <br>
<pre>
    def search(self,value):
        index = 0
        if(self.head!=None):
            current = self.head
            while (index < self.__size ):
                if current.value == value:
                    return index
                current = current.next
                index = index + 1
        return -1
</pre>
</details>
  

# Data Structures Tutorial PART 2

## Queues 🚶🚶‍♀️🚶🏿‍♀️🚶🚶🏿‍♂️

Formally speaking, a Queue [*"is a linear structure which follows a particular order in which the operations are performed."*](https://www.geeksforgeeks.org/queue-data-structure/) The order of organization of the items that compose the queue is First In First Out (FIFO).The following imagen shows a graphic representatios of the queue.
<details>
  <summary><span>Linear Data Structure</span></summary>
  
  <span>*A data structure is linear if it's elements are connected and arranged to each other in a sequential manner allowing the elemnts to be ordered.*</span>
</details>

<img src="./queue.jpg"/>

## Real-life example - Bank queue 💰

<img src="./bank-queue.jpg"/>

When you see a bank queue, what are the first things that you identify? Possibly you can see queues where each member has a number that determine the turns or they just align in a row and keep the order that way. In both cases the person in the head of the queue is the first to be attended, the queue is reduced one by one, however, exist some cases where the usual norm change, such is the case of **priority queues** where the values to be stored have a certain priority level respect others, this priority can affect the order when a new value is inserted.

<img style="width:80%; height=60%" src="./bank.jpg"/>


## **Queue implementation with Python Code**

To model a queue we use the same logic applied to the Linked List, we need to use nodes to store the data and link them through pointers. The difference between the Linked List and the queue lies in the fact that queues follow an specific behavior like the FIFO.

### Attributes

- lenght : INTEGER       -> number of elements in the queue.
- first  : NODE          -> Pointer to the first node of the queue
- last   : NODE          -> Pointer to the last node of the queue

```
class Queue:
    class Node:
        def __init__(self,value):
            self.value = value
            self.next = None
            self.before = None
        
    def __init__(self):
        self.__lenght = 0
        self.first = None
        self.last = None
```
### Functions

- enqueue() store/add/insert a new element into the last position of the queue

```
    def enqueue(self, value):
        # Verify first if the Queue is empty
        # If is not empty walk through each node until you find the last node  (´next´ value equals to null pointer)
        # in other case, initialize the first of the Queue
        if(self.first!=None):
            current = self.first
            aux = self.first.next
            stop = False
            while (not stop ):
                if(aux==None):
                    # create new node
                    current.next = Queue.Node(value)
                    # make the last point to the new node
                    self.last = current.next
                    self.last.prev = current
                    stop = True
                else:
                    current = aux
                    aux = current.next
        else:
            self.first = Queue.Node(value)
            self.last = self.first
        self.__lenght = self.__lenght+1
```

- dequeue() delete/remove the first element of the queue

```
    def dequeue(self):
        # Verify first if the Queue is empty
        # If is not empty walk through each node until find the last node  
        # and remove it from the queue
        node = self.first
        if (self.__lenght > 0):
            if(self.last!=None):
                if(self.__lenght > 1):
                    current = self.first.next
                    current.previous = None
                    self.first = current
                elif(self.__lenght == 1):
                    self.first == None
                    self.last == None
            self.__lenght = self.__lenght-1
        return node
```

## Homework

Rewrite the queue class and functions to work as a priority queue.

- The queue stores Integer values.
- Add a new attirbute "priority" to the queue that will have one of two values: "regular" or "vip"
- "vip" numbers have priority over the "regular" numbers, however, they keep the respective FIFO order between them.

Example if you insert (24, regular),(12, vip),(3, regular), and (1,vip) respectively, and print the queue the value should display (12 1 24 3).
  
  

