// Objective: Implementation of a generic Queue using a Linked List.
// Operations: enqueue, dequeue, front, rear, clearQueue, search, display.
// Time Complexity: O(1) for enqueue, dequeue, front, rear | O(n) for clearQueue, search, display
// Space Complexity: O(n) dynamic memory

#include <iostream>
#include <cassert>

using namespace std;

template<class t>
class linkedQueue
{
private:
	struct Node
	{
		t item;
		Node *next;
	};
	int length;
	Node *frontPtr, *rearPtr;

public:
	// Constructor: Initialize empty queue
	linkedQueue() : frontPtr(NULL), rearPtr(NULL), length(0) {}

	// Check if queue has no elements
	bool isEmpty()
	{
		return (length == 0);
	}

	// Insert element at the rear (Enqueue)
	void enqueue(t item)
	{
		Node *newNode = new Node;
		newNode->item = item;
		newNode->next = NULL;

		if (length == 0)
			rearPtr = frontPtr = newNode;
		else
		{
			rearPtr->next = newNode;
			rearPtr = newNode;
		}
		length++;
	}

	// Remove element from the front (Dequeue)
	void dequeue()
	{
		if (isEmpty())
			cout << "Empty Queue\n";
		else if (length == 1)
		{
			delete frontPtr;
			frontPtr = rearPtr = NULL;
			length = 0;
		}
		else
		{
			Node *current = frontPtr;
			frontPtr = frontPtr->next;
			delete current;
			length--;
		}
	}

	// Get value of front element
	t front()
	{
		assert(!isEmpty());
		return frontPtr->item;
	}

	// Get value of rear element
	t rear()
	{
		assert(!isEmpty());
		return rearPtr->item;
	}

	// Remove all elements and free memory
	void clearQueue()
	{
		Node *current;
		while (frontPtr != NULL)
		{
			current = frontPtr;
			frontPtr = frontPtr->next;
			delete current;
		}
		rearPtr = NULL;
		length = 0;
	}

	// Display all elements from front to rear
	void display()
	{
		Node *cur = frontPtr;
		cout << "Item in the queue: [ ";
		while (cur != NULL)
		{
			cout << cur->item << " ";
			cur = cur->next;
		}
		cout << "]\n";
	}

	// Search for an element in the queue
	void search(t item)
	{
		Node *cur = frontPtr;
		bool found = false;

		while (cur != NULL)
		{
			if (cur->item == item)
			{
				cout << "The item: " << item << " is found\n";
				found = true;
				break;
			}
			cur = cur->next;
		}
		if (!found)
			cout << "The item: " << item << " is not found\n";
	}

	// Destructor: Clean up allocated nodes
	~linkedQueue()
	{
		clearQueue();
	}
};

int main()
{
	linkedQueue<int> q1;

	for (int i = 1; i <= 20; i++)
		q1.enqueue(i);

	cout << "Front: " << q1.front() << endl;
	cout << "Rear: " << q1.rear() << endl;
	q1.display();

	return 0;
}
