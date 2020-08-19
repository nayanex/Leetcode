# 232. Implement Queue using Stacks

https://leetcode.com/problems/implement-queue-using-stacks/


## My Solution

```python
class Stack:
    def __init__(self):
        self.data = []
        
    def push(self, x: int) -> None:
        self.data.append(x)

    def pop(self) -> int:
        return self.data.pop()
    
    def is_empty(self) -> bool:
        return not self.data
    
    def peek(self) -> int:
        return self.data[-1]
    
    def __str__(self) -> str:
        return str(self.data)
    
class MyQueue:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.stack_new = Stack()
        self.stack_old = Stack()
        

    def push(self, x: int) -> None:
        """
        Push element x to the back of queue.
        """
        self.stack_old.push(x)
        

    def pop(self) -> int:
        """
        Removes the element from in front of queue and returns that element.
        """
        self.__shif_stacks()
        return self.stack_new.pop()
        

    def peek(self) -> int:
        """
        Get the front element.
        """
        self.__shif_stacks()
        return self.stack_new.peek()
        

    def empty(self) -> bool:
        """
        Returns whether the queue is empty.
        """
        return self.stack_new.is_empty() and self.stack_old.is_empty()
        
    def __shif_stacks(self) -> None:
        if self.stack_new.is_empty():
            while not self.stack_old.is_empty():
                self.stack_new.push(self.stack_old.pop())
        


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```
