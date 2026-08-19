// Objective: Implementation of a Doubly Linked List with forward/backward traversal and position-based/value-based operations.
// Operations: insertFirst, insertLast, insertAt, removeFirst, removeLast, deleteNthNode, remove, display, reverse_display, destroy.
// Time Complexity: O(1) for insertFirst, insertLast, removeFirst, removeLast | O(n) for insertAt, deleteNthNode, remove, display, reverse_display
// Space Complexity: O(n) dynamic memory

#include<iostream>
using namespace std;

class doublyLinkedList {
private:
	struct Node {
		int item;
		Node* next;
		Node* prev;
	};
	Node* first;
	Node* last;
	int count;

public:
	// Constructor: Initialize empty doubly linked list
	doublyLinkedList() {
		first = NULL;
		last = NULL;
		count = 0;
	}

	// Check if list is empty
	bool isEmpty() {
		return (first == NULL);
	}

	// Free all allocated nodes
	void destroy() {
		Node *temp;
		while (first != NULL) {
			temp = first;
			first = first->next;
			delete temp;
		}
		last = NULL;
		count = 0;
	}

	// Insert element at the end
	void insertLast(int val) {
		Node* newNode = new Node;
		newNode->item = val;
		if (count == 0) {
			first = last = newNode;
			newNode->next = newNode->prev = NULL;
		}
		else {
			newNode->next = NULL;
			newNode->prev = last;
			last->next = newNode;
			last = newNode;
		}
		count++;
	}

	// Insert element at the beginning
	void insertFirst(int item) {
		Node* newNode = new Node;
		newNode->item = item;
		if (count == 0) {
			first = last = newNode;
			newNode->next = newNode->prev = NULL;
		}
		else {
			newNode->next = first;
			newNode->prev = NULL;
			first->prev = newNode;
			first = newNode;
		}
		count++;
	}

	// Insert element at a specific index
	void insertAt(int pos, int item) {
		if (pos < 0 || pos > count)
			cout << "Out Of Range ...!\n";
		else {
			if (pos == 0)
				insertFirst(item);
			else if (pos == count)
				insertLast(item);
			else {
				Node *newNode = new Node;
				newNode->item = item;
				Node *current = first;
				for (int i = 1; i < pos; i++) {
					current = current->next;
				}

				newNode->next = current->next;
				newNode->prev = current;
				current->next->prev = newNode;
				current->next = newNode;
				count++;
			}
		}
	}

	// Remove first element
	void removeFirst() {
		if (count == 0)
			cout << "Empty List\n";
		else if (count == 1) {
			delete first;
			last = first = NULL;
			count--;
		}
		else {
			Node* current = first;
			first = first->next;
			first->prev = NULL;
			delete current;
			count--;
		}
	}

	// Remove last element
	void removeLast() {
		if (count == 0)
			cout << "Empty List\n";
		else if (count == 1) {
			delete first;
			last = first = NULL;
			count--;
		}
		else {
			Node *current = last;
			last = last->prev;
			last->next = NULL;
			delete current;
			count--;
		}
	}

	// Delete node at specific index
	void deleteNthNode(int pos) {
		if (pos < 0 || pos >= count) {
			cout << "Out Of Range\n";
			return;
		}
		else if (pos == 0) {
			removeFirst();
		}
		else if (pos == count - 1) {
			removeLast();
		}
		else {
			Node *current = first->next;
			for (int i = 1; i < pos; i++) {
				current = current->next;
			}
			current->prev->next = current->next;
			current->next->prev = current->prev;
			delete current;
			count--;
		}
	}

	// Remove element by value
	void remove(int item) {
		if (isEmpty()) {
			cout << "Empty List Can't Remove\n";
			return;
		}

		if (first->item == item) {
			removeFirst();
			return;
		}
		else {
			Node* current = first->next;
			while (current != NULL) {
				if (current->item == item)
					break;
				current = current->next;
			}

			if (current == NULL) {
				cout << "The item is not there\n";
				return;
			}
			else if (current->next == NULL) {
				removeLast();
				return;
			}
			else {
				current->prev->next = current->next;
				current->next->prev = current->prev;
				delete current;
				count--;
			}
		}
	}

	// Print elements from first to last
	void display() {
		if (isEmpty()) {
			cout << "Empty List Can't Display...!\n";
		}
		else {
			Node* temp = first;
			cout << "Forward: [ ";
			while (temp != nullptr) {
				cout << temp->item << " ";
				temp = temp->next;
			}
			cout << "]\n";
		}
	}

	// Print elements in reverse order from last to first
	void reverse_display() {
		if (isEmpty()) {
			cout << "Empty List Can't Display Reverse...!\n";
		}
		else {
			Node* temp = last;
			cout << "Backward: [ ";
			while (temp != NULL) {
				cout << temp->item << " ";
				temp = temp->prev;
			}
			cout << "]\n";
		}
	}

	// Destructor: Free allocated memory
	~doublyLinkedList() {
		destroy();
	}
};

int main() {
	doublyLinkedList dl;
	dl.insertAt(0, 4);
	dl.insertAt(1, 6);
	dl.insertAt(2, 7);
	dl.insertFirst(2);
	dl.insertLast(10);
	dl.remove(7);

	dl.display();
	dl.reverse_display();

	return 0;
}
