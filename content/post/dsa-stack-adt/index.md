---
title: Stack ADT 實作
description: 關於 Stack push、pop、peek、isEmpty、isFull
date: 2023-12-08 00:00:00+0000
categories:
    - DS
---

##  Stack ADT

* 使用 Array
* 使用 LinkedList

### 使用 Array 實作

```java

public class StackADT {
    private int maxSize;
    private int[] stackArray;
    private int top;

    public StackADT(int size) {
        maxSize = size;
        stackArray = new int[maxSize];
        top = -1; // stack是空時，top = -1
    }

    public void push(int value) {
        if (top < maxSize -1) { // 先檢查是否已滿
            top++;
            stackArray[top] = value; // 先增加 top，然後儲存值
        } else {
            throw new RuntimeException("Stack is full.")
        }
    }

    public int pop() {
        if (top >= 0) { //檢查stack頂是否為空
            return stackArray[top--]; // stack 減小top
        } else {
            throw new RuntimeException("Stack is empty. Cannot pop.");
        }
    }

    public int peek() {
        if (top >= 0) {
            return stackArray[top]; // 返回stack頂，但不pop
        } else {
            throw new RuntimeException("Stack is empty. Cannot peek.");
        }
    }

    // 檢查是否空
    public boolean isEmpty() {
        return top == -1;
    }

    // 檢查是否已滿
    public boolean isFull() {
        return top == maxSize - 1;
    }

    

}

```


#### C++ 實做

```C++
#include <iostream>
#include <vector>

class MyStack {
public:
    MyStack() {
        maxSize = 100;
        stackArray.resize(maxSize);
        top = -1;
    }

    void push(int value) {
        if (top < maxSize - 1) {
            stackArray[++top] = value;
        } else {
            throw std::runtime_error("Stack is full.");
        }
    }

    int pop() {
        if (!isEmpty()) {
            return stackArray[top--];
        } else {
            throw std::runtime_error("Stack is empty.");
        }
    }

    int peek() {
        if (!isEmpty()) {
            return stackArray[top];
        } else {
            throw std::runtime_error("Stack is empty.");
        }
    }

    bool isEmpty() {
        return top == -1;
    }

    int size() {
        return top + 1;
    }

private:
    std::vector<int> stackArray; 
    int maxSize;
    int top;
};

int main() {
    MyStack intStack;
    
    intStack.push(1);
    intStack.push(2);
    intStack.push(3);

    int topElement = intStack.pop();

    bool isEmpty = intStack.isEmpty();

    int stackSize = intStack.size();

    std::cout << "Top element: " << topElement << std::endl;
    std::cout << "Stack is empty: " << (isEmpty ? "true" : "false") << std::endl;
    std::cout << "Stack size: " << stackSize << std::endl;

    return 0;
}
```