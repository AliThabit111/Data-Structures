/**
 * @file stack_array.cpp
 * @brief Implementation of a generic Stack data structure using a static array.
 * 
 * Objectives:
 * - Implement standard LIFO (Last In, First Out) operations from scratch.
 * - Support generic data types using C++ Class Templates.
 * - Demonstrate boundary condition handling (Stack Overflow and Underflow).
 * 
 * Time Complexities:
 * - push(element) : O(1)
 * - pop()          : O(1)
 * - getTop()       : O(1)
 * - isEmpty()      : O(1)
 * - print()        : O(n)
 * 
 * Space Complexity: O(MAX_SIZE) for static memory allocation.
 */

#include <iostream>

const int MAX_SIZE = 100; // Define maximum capacity for the stack

template <class T>
class Stack {
private:
    int top;
    T item[MAX_SIZE];

public:
    // Constructor: Initialize the stack as empty
    Stack() : top(-1) {}

    // Check whether the stack is empty
    bool isEmpty() const {
        return top < 0;
    }

    // Check whether the stack is full
    bool isFull() const {
        return top >= MAX_SIZE - 1;
    }

    // Push an element onto the top of the stack
    void push(T element) {
        if (isFull()) {
            std::cout << "Error: Stack overflow on push\n";
            return;
        }
        item[++top] = element;
    }

    // Remove the topmost element without returning it
    void pop() {
        if (isEmpty()) {
            std::cout << "Error: Stack underflow on pop\n";
            return;
        }
        top--;
    }

    // Remove the topmost element and assign its value to the passed reference
    void pop(T &element) {
        if (isEmpty()) {
            std::cout << "Error: Stack underflow on pop\n";
            return;
        }
        element = item[top--];
    }

    // Retrieve the value of the top element without removing it
    void getTop(T &stackTop) const {
        if (isEmpty()) {
            std::cout << "Error: Stack is empty on getTop\n";
            return;
        }
        stackTop = item[top];
        std::cout << "Top Element: " << stackTop << "\n";
    }

    // Display all elements in the stack from top to bottom
    void print() const {
        if (isEmpty()) {
            std::cout << "Stack is empty: [ ]\n";
            return;
        }
        std::cout << "[ ";
        for (int i = top; i >= 0; i--) {
            std::cout << item[i] << " ";
        }
        std::cout << "]\n";
    }
};

int main() {
    Stack<int> s;

    // Push elements into the stack
    s.push(5);
    s.push(15);
    s.push(20);

    std::cout << "Current Stack elements:\n";
    s.print();

    // Check top element
    int topVal;
    s.getTop(topVal);

    // Pop element
    int poppedVal;
    s.pop(poppedVal);
    std::cout << "Popped: " << poppedVal << "\n";

    std::cout << "Stack after pop:\n";
    s.print();

    return 0;
}
