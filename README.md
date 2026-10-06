# stack-and-queue-implementations
Data structures implementations: Stack using array and Circular Queue using array
Question 1 – Stack Using Array
Problem Statement
Design and implement a stack using an array without using any built-in stack library.

The program supports:

PUSH(x)
POP()
PEEK()
DISPLAY()
The program also handles Stack Overflow and Stack Underflow conditions.

Theory
A stack is a linear data structure that follows the LIFO (Last In, First Out) principle. The element inserted last is the first element to be removed.

In an array implementation, a variable called top keeps track of the top element of the stack.
• push(x): Adds element x to the top of the stack.
• pop(): Removes and returns the top element.
• peek() or top(): Returns the top element without removing it.
• isEmpty(): Returns true if the stack contains no elements.
• isFull(): Returns true if the array capacity is maxed out.

Initially:

top = -1
When an element is pushed, top is increased and the element is stored at that position.

When an element is popped, the element at top is removed and top is decreased.

Operations
PUSH(x)
Adds an element to the top of the stack.

If top == MAX - 1, the stack is already full and Stack Overflow occurs.

POP()
Removes the top element from the stack.

If top == -1, the stack is empty and Stack Underflow occurs.

PEEK()
Displays the top element without removing it.

DISPLAY()
Displays all elements currently present in the stack from top to bottom.

Complexity Analysis
Operation	Time Complexity	Space Complexity
PUSH	O(1)	O(1)
POP	O(1)	O(1)
PEEK	O(1)	O(1)
DISPLAY	O(n)	O(1)
The overall stack requires O(n) space for an array of capacity n.

Fixed Stack Size and Overflow
The stack in this program has a fixed capacity of 5 elements.

If the stack is full and the user attempts to insert another element, the program does not insert the element. Instead, it displays a Stack Overflow message.

This happens because an array with fixed size cannot store elements beyond its allocated capacity.

Source Code
The complete program is available in:
Question 2 – Circular Queue Using Array
Problem Statement
Implement a circular queue using an array.

The program supports:

ENQUEUE(x)
DEQUEUE()
FRONT()
DISPLAY()
The implementation correctly distinguishes between a full queue and an empty queue.

Theory
A queue is a linear data structure that follows the FIFO (First In, First Out) principle. The element inserted first is removed first.

A circular queue treats the last position of the array as connected to the first position. Therefore, when rear reaches the last index, it can wrap around to the beginning of the array.

The circular movement is implemented using:

(rear + 1) % MAX
and:

(front + 1) % MAX
Operations
ENQUEUE(x)
Adds an element at the rear of the queue.

The queue is considered full when:

(rear + 1) % MAX == front
DEQUEUE()
Removes an element from the front of the queue.

If the queue contains only one element, both front and rear are reset to -1.

FRONT()
Displays the element currently at the front without removing it.

DISPLAY()
Displays all elements from front to rear, including elements that wrap around to the beginning of the array.

Circular Queue vs Linear Queue
Feature	Linear Queue	Circular Queue
Memory utilization	Can leave unused positions at the beginning	Reuses freed positions
Movement of rear	Moves only forward	Wraps around
ENQUEUE	O(1)	O(1)
DEQUEUE	O(1)	O(1)
Space	O(n)	O(n)
Reuses deleted positions	Not efficiently in a simple array implementation	Yes
1. Why does a circular queue provide better memory utilization?
In a simple linear queue, after elements are removed from the front, those positions may remain unused even though there is free space.

A circular queue solves this problem by allowing rear to wrap around to the beginning of the array and reuse those positions.

Complexity Analysis
Operation	Time Complexity	Space Complexity
push()	\(\mathcal{O}(1)\)	\(\mathcal{O}(1)\)
pop()	\(\mathcal{O}(1)\)	\(\mathcal{O}(1)\)
peek()	\(\mathcal{O}(1)\)	\(\mathcal{O}(1)\)
Overall Space	—	\(\mathcal{O}(N)\) (where N is array capacity)
2. Time Complexity
ENQUEUE → O(1)
DEQUEUE → O(1)
FRONT → O(1)
DISPLAY → O(n)
3. Space Complexity
A circular queue using an array of capacity n requires O(n) space.

4. Problem in a Linear Queue
Suppose a linear queue has five positions:

[10][20][30][40][50]
After removing the first three elements:

[ ][ ][ ][40][50]
The first three positions are unused, but rear is already at the last index.

In a simple linear array implementation, another element cannot be inserted even though free positions exist at the beginning. This is the false overflow / wasted-space problem that a circular queue avoids.
python
class MyStack:
    def __init__(self, size: int):
        self.capacity = size
        # Pre-allocate array with None to simulate a fixed-size array
        self.arr = [None] * size
        self.top = -1  # -1 indicates that the stack is initially empty

    def push(self, x: int) -> None:
        if self.is_full():
            print(f"Stack Overflow! Cannot push {x}")
            return
        self.top += 1
        self.arr[self.top] = x
        print(f"Pushed: {x}")

    def pop(self) -> int:
        if self.is_empty():
            print("Stack Underflow! Cannot pop.")
            return -1
        popped_element = self.arr[self.top]
        self.arr[self.top] = None  # Optional: Clear the reference
        self.top -= 1
        return popped_element

    def peek(self) -> int:
        if self.is_empty():
            print("Stack is empty.")
            return -1
        return self.arr[self.top]

    def is_empty(self) -> bool:
        return self.top == -1

    def is_full(self) -> bool:
        return self.top == self.capacity - 1


# Driver code to demonstrate the stack behavior
if __name__ == "__main__":
    stack = MyStack(3)  # Create a stack of size 3

    stack.push(10)
    stack.push(20)
    stack.push(30)
    stack.push(40)  # Triggers Stack Overflow

    print("Top element is:", stack.peek())

    print("Popped element:", stack.pop())
    print("Top element after pop:"

Source Code
The complete program is available in:

Q2_Circular_Queue/circular_queue.c
Circular Queue is an extended version of a regular queue that connects the last position back to the first position to form a circle, efficiently utilizing wasted memory space.

How to Compile and Run
Stack
Open a terminal in the Q1_Stack folder and run:

gcc stack.c -o stack
Then:

./stack
On Windows, you can run:

stack.exe
Circular Queue
Open a terminal in the Q2_Circular_Queue folder and run:
python
class CircularQueue:
    def __init__(self, size):
        self.size = size
        self.queue = [None] * size
        self.front = -1
        self.rear = -1

    def is_full(self):
        if (self.front == 0 and self.rear == self.size - 1) or (self.front == self.rear + 1):
            return True
        return False

    def is_empty(self):
        if self.front == -1:
            return True
        return False

    def enqueue(self, data):
        if self.is_full():
            print("Queue is full!")
        else:
            if self.front == -1:
                self.front = 0
            self.rear = (self.rear + 1) % self.size
            self.queue[self.rear] = data
            print(f"Inserted -> {data}")

    def dequeue(self):
        if self.is_empty():
            print("Queue is empty!")
            return None
        else:
            temp = self.queue[self.front]
            if self.front == self.rear:
                self.front = -1
                self.rear = -1
            else:
                self.front = (self.front + 1) % self.size
            return temp

    def display(self):
        if self.is_empty():
            print("Empty Queue")
        else:
            print(f"Front -> {self.front}")
            print("Items -> ", end="")
            
            index = self.front
            while True:
                print(self.queue[index], end=" ")
                if index == self.rear:
                    break
                index = (index + 1) % self.size
            print(f"\nRear -> {self.rear}")


# Driver Code
if __name__ == "__main__":
    cq = CircularQueue(5)

    # Failing dequeue on empty queue
    cq.dequeue()

    cq.enqueue(10)
    cq.enqueue(20)
    cq.enqueue(30)
    cq.enqueue(40)
    cq.enqueue(50)

    # Fails to enqueue because queue is full
    cq.enqueue(60)

    cq.display()

    print(f"Deleted element -> {cq.dequeue()}")

    cq.display()

    cq.enqueue(60)
    cq.display()

gcc circular_queue.c -o circular_queue
Then:

./circular_queue
On Windows:

circular_queue.exe
