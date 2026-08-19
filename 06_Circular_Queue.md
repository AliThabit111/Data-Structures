// Objective: Implementation of a Circular Queue using dynamic array.
// Operations: addQueue (enqueue), deleteQueue (dequeue), frontQueue, rearQueue, queueSearch, printQueue.
// Time Complexity: O(1) for enqueue, dequeue, front, rear | O(n) for print and search
// Space Complexity: O(n) based on allocated capacity

#include <iostream>
#include <cassert>

using namespace std;

class arrayQueueType
{
	int rear;
	int front;
	int length;
	int *arr;
	int maxSize;

public:
	// Constructor: Initialize queue with custom size
	arrayQueueType(int size) {
		if (size <= 0)
			maxSize = 100;
		else
			maxSize = size;

		front = 0;
		arr = new int[maxSize];
		rear = maxSize - 1;
		length = 0;
	}

	// Check if queue has no elements
	int isEmpty() {
		return length == 0;
	}

	// Check if queue is full
	bool isFull() {
		return length == maxSize;
	}

	// Insert element at the rear (Enqueue)
	void addQueue(int Element) {
		if (isFull()) {
			cout << "Queue Full Can't Enqueue ...!\n";
		}
		else {
			rear = (rear + 1) % maxSize;
			arr[rear] = Element;
			length++;
		}
	}

	// Remove element from the front (Dequeue)
	void deleteQueue() {
		if (isEmpty()) {
			cout << "Empty Queue Can't Dequeue ...!\n";
		}
		else {
			front = (front + 1) % maxSize;
			--length;
		}
	}

	// Get front element
	int frontQueue() {
		assert(!isEmpty());
		return arr[front];
	}

	// Get rear element
	int rearQueue() {
		assert(!isEmpty());
		return arr[rear];
	}

	// Print all elements in circular order
	void printQueue() {
		if (!isEmpty()) {
			cout << "[ ";
			for (size_t i = front; i != rear; i = (i + 1) % maxSize) {
				cout << arr[i] << " ";
			}
			cout << arr[rear] << " ]\n";
		}
		else {
			cout << "Empty Queue\n";
		}
	}

	// Search for an element and return its index
	int queueSearch(int element) {
		int pos = -1;
		if (!isEmpty()) {
			for (int i = front; i != rear; i = (i + 1) % maxSize) {
				if (arr[i] == element) {
					pos = i;
					break;
				}
			}
			if (pos == -1) {
				if (arr[rear] == element)
					pos = rear;
			}
		}
		else {
			cout << "Queue is empty!\n";
		}
		return pos;
	}

	// Destructor: Free allocated memory
	~arrayQueueType() {
		delete[] arr;
	}
};

int main()
{
	arrayQueueType q1(5);
	q1.addQueue(10);
	q1.addQueue(20);
	q1.addQueue(30);
	q1.addQueue(40);
	q1.addQueue(50);
	q1.printQueue();

	return 0;
}
