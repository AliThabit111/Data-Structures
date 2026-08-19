
 * Objective: Implementation of a dynamic Stack using a Singly Linked List with template support.
 * Operations: push, pop, getTop, isEmpty, display
 * Time Complexity: O(1) for push, pop, getTop | O(n) for display
 * Space Complexity: O(n) dynamic memory


#include<iostream>
using namespace std;

template<class t>
class Stack {
private:
	struct StackNode {
		t item;
		StackNode* next;
	};
	StackNode *topPtr, *curPtr;

public:
	// Constructor to initialize empty stack
	Stack() {
		topPtr = NULL;
	}

	// Check if stack is empty
	bool isEmpty() {
		return topPtr == NULL;
	}

	// Insert element at the top
	void push(t newItem) {
		StackNode *newPtr = new StackNode;
		if (newPtr == NULL)
			cout << "Stack push cannot allocate memory\n";
		else {
			newPtr->item = newItem;
			newPtr->next = topPtr;
			topPtr = newPtr;
		}
	}

	// Remove top element
	void pop() {
		if (isEmpty())
			cout << "Stack empty on pop\n";
		else {
			StackNode *temp = topPtr;
			topPtr = topPtr->next;
			temp->next = NULL;
			delete temp;
		}
	}

	// Remove top element and return value by reference
	void pop(t& stackTop) {
		if (isEmpty())
			cout << "Stack empty on pop\n";
		else {
			stackTop = topPtr->item;
			StackNode *temp = topPtr;
			topPtr = topPtr->next;
			temp->next = NULL;
			delete temp;
		}
	}

	// Get the top element value
	void getTop(t& stackTop) {
		if (isEmpty())
			cout << "stack empty on getTop\n";
		else {
			stackTop = topPtr->item;
			cout << "\nTop Element of the stack is " << stackTop << endl;
		}
	}

	// Display all elements from top to bottom
	void display() {
		curPtr = topPtr;
		cout << "\nItems in the stack : [ ";
		while (curPtr != NULL) {
			cout << curPtr->item << " ";
			curPtr = curPtr->next;
		}
		cout << "]\n";
	}
};

int main() {
	Stack<int> s;
	s.push(10);
	s.push(20);
	s.push(30);
	s.display();

	return 0;
}
