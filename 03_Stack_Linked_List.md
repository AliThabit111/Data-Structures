/**
 * @file stack_linked_list.cpp
 * @brief Implementation of a dynamic Stack using a Singly Linked List in C++.
 * 
 * Objectives:
 * - Implement standard LIFO (Last In, First Out) operations with dynamic memory.
 * - Eliminate capacity restrictions (no fixed MAX_SIZE).
 * - Proper heap allocation and deallocation to prevent memory leaks.
 * 
 * Time Complexities:
 * - push(newItem)  : O(1)
 * - pop()          : O(1)
 * - getTop()       : O(1)
 * - isEmpty()      : O(1)
 * - display()      : O(n)
 * 
 * Space Complexity: O(n) where n is the number of active nodes.
 */

#include <iostream>

template <class T>
class Stack {
private:
    struct StackNode {
        T item;
        StackNode* next;
    };

    StackNode* topPtr;

public:
    // Constructor: Initialize the stack as empty
    Stack() : topPtr(nullptr) {}

    // Destructor: Clean up all dynamically allocated nodes
    ~Stack() {
        while (!isEmpty()) {
            pop();
        }
    }

    // Check whether the stack is empty
    bool isEmpty() const {
        return topPtr == nullptr;
    }

    // Insert an item at the top of the stack
    void push(T newItem) {
        StackNode* newPtr = new (std::nothrow) StackNode;
        if (newPtr == nullptr) {
            std::cout << "Error: Memory allocation failed on push\n";
            return;
        }
        newPtr->item = newItem;
        newPtr->next = topPtr;
        topPtr = newPtr;
    }

    // Remove the topmost element without returning it
    void pop() {
        if (isEmpty()) {
            std::cout << "Error: Stack underflow on pop\n";
            return;
        }
        StackNode* temp = topPtr;
        topPtr = topPtr->next;
        delete temp;
    }

    // Remove the topmost element and assign its value to the passed reference
    void pop(T& stackTop) {
        if (isEmpty()) {
            std::cout << "Error: Stack underflow on pop\n";
            return;
        }
        stackTop = topPtr->item;
        StackNode* temp = topPtr;
        topPtr = topPtr->next;
        delete temp;
    }

    // Retrieve the top element without removing it
    void getTop(T& stackTop) const {
        if (isEmpty()) {
            std::cout << "Error: Stack is empty on getTop\n";
            return;
        }
        stackTop = topPtr->item;
        std::cout << "Top Element of the stack is: " << stackTop << "\n";
    }

    // Print all elements from top to bottom
    void display() const {
        if (isEmpty()) {
            std::cout << "Stack is empty: [ ]\n";
            return;
        }

        StackNode* curPtr = topPtr;
        std::cout << "Items in the stack: [ ";
        while (curPtr != nullptr) {
            std::cout << curPtr->item << " ";
            curPtr = curPtr->next;
        }
        std::cout << "]\n";
    }
};

int main() {
    Stack<int> s;

    // Push elements
    s.push(10);
    s.push(20);
    s.push(30);

    // Display stack
    s.display();

    // Check top
    int topItem;
    s.getTop(topItem);

    // Pop element
    int poppedItem;
    s.pop(poppedItem);
    std::cout << "Popped item: " << poppedItem << "\n";

    // Display stack after pop
    s.display();

    return 0;
}
