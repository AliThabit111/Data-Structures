
 * Objective: Implementation of a Stack using a static array with template support.
 * Operations: push, pop, getTop, isEmpty, print
 * Time Complexity: O(1) for push, pop, getTop | O(n) for print
 * Space Complexity: O(MAX_SIZE)
 */

#include<iostream>
using namespace std;

const int MAX_SIZE = 100;

template<class t>
class stack {
	int top;
	t item[MAX_SIZE];
public:
	// Constructor to initialize empty stack
	stack() : top(-1) {}

	// Check if stack has no elements
	bool isEmpty() {
		return top < 0;
	}

	// Insert element at the top
	void push(t Element) {
		if (top >= MAX_SIZE - 1) {
			cout << "Stack full on push\n";
		}
		else {
			top++;
			item[top] = Element;
		}
	}

	// Remove top element
	void pop() {
		if (isEmpty())
			cout << "stack empty on pop\n";
		else
			top--;
	}

	// Remove top element and return its value by reference
	void pop(t& Element) {
		if (isEmpty())
			cout << "stack empty on pop\n";
		else {
			Element = item[top];
			top--;
		}
	}

	// Get the value of the top element
	void getTop(t& stackTop) {
		if (isEmpty())
			cout << "stack empty on getTop\n";
		else {
			stackTop = item[top];
			cout << stackTop << endl;
		}
	}

	// Display all elements from top to bottom
	void print() {
		cout << "[ ";
		for (int i = top; i >= 0; i--) {
			cout << item[i] << " ";
		}
		cout << "]\n";
	}
};

int main() {
	stack<int> s;
	s.push(5);
	s.push(15);
	s.push(20);
	s.print();

	return 0;
}
