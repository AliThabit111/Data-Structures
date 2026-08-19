// Objective: Implementation of a Singly Linked List with full CRUD operations, ordering, and reversal.
// Operations: insertFirst, insertEnd, insertAt, insertOrdered, removeFirst, removeLast, removeAt, remove, seqSearch, reverse, clearList, print.
// Time Complexity: O(1) for insertFirst, insertEnd, removeFirst | O(n) for insertAt, removeLast, removeAt, seqSearch, reverse, print
// Space Complexity: O(n) dynamic memory

#include <iostream>
using namespace std;

struct nodeType
{
	int info;
	nodeType *next;
};

class linkedListType
{
public:
	linkedListType();
	int listSize();
	bool isEmpty();
	int seqSearch(int);
	void remove(int);
	void insertFirst(int);
	void insertEnd(int);
	void insertAt(int, int);
	void removeAt(int);
	void print();
	void clearList();
	void insertOrdered(int);
	void removeFirst();
	void removeLast();
	void removeLast2();
	int removeOddSumEven();
	void reverse();
	~linkedListType();

private:
	nodeType *first, *last;
	int length;
};

// Constructor: Initialize empty list
linkedListType::linkedListType()
{
	first = last = NULL;
	length = 0;
}

// Return current number of elements
int linkedListType::listSize()
{
	return length;
}

// Check if list is empty
bool linkedListType::isEmpty()
{
	return (length == 0);
}

// Insert element at the beginning
void linkedListType::insertFirst(int item)
{
	nodeType *newNode = new nodeType;
	newNode->info = item;
	if (length == 0) {
		first = last = newNode;
		newNode->next = NULL;
	}
	else {
		newNode->next = first;
		first = newNode;
	}
	length++;
}

// Insert element at the end
void linkedListType::insertEnd(int item)
{
	nodeType *newNode = new nodeType;
	newNode->info = item;
	newNode->next = NULL;

	if (length == 0) {
		first = last = newNode;
	}
	else {
		last->next = newNode;
		last = newNode;
	}
	length++;
}

// Insert element at a specific index
void linkedListType::insertAt(int loc, int item)
{
	if (loc < 0 || loc > length)
		cout << "ERROR: Out of range\n";
	else
	{
		if (loc == 0)
			insertFirst(item);
		else if (loc == length)
			insertEnd(item);
		else
		{
			nodeType *newNode = new nodeType;
			newNode->info = item;
			nodeType *current = first;
			for (int i = 1; i < loc; i++)
				current = current->next;

			newNode->next = current->next;
			current->next = newNode;
			length++;
		}
	}
}

// Insert element while keeping the list sorted in ascending order
void linkedListType::insertOrdered(int item)
{
	nodeType *newNode = new nodeType;
	newNode->info = item;

	if (first == NULL)
	{
		first = last = newNode;
		newNode->next = NULL;
		length++;
	}
	else if (first->info >= item)
	{
		newNode->next = first;
		first = newNode;
		length++;
	}
	else
	{
		nodeType *current = first->next;
		nodeType *trailCurrent = first;

		while (current != NULL)
		{
			if (current->info >= item)
				break;
			current = current->next;
			trailCurrent = trailCurrent->next;
		}
		if (current == NULL)
		{
			last->next = newNode;
			newNode->next = NULL;
			last = newNode;
			length++;
		}
		else
		{
			trailCurrent->next = newNode;
			newNode->next = current;
			length++;
		}
	}
}

// Remove first element
void linkedListType::removeFirst()
{
	if (length == 0)
		cout << "ERROR: EMPTY LIST\n";
	else if (length == 1)
	{
		delete first;
		last = first = NULL;
		length--;
	}
	else
	{
		nodeType *current = first;
		first = first->next;
		delete current;
		length--;
	}
}

// Remove last element using two pointers
void linkedListType::removeLast()
{
	if (length == 0)
		cout << "ERROR: EMPTY LIST\n";
	else if (length == 1)
	{
		delete first;
		last = first = NULL;
		length--;
	}
	else
	{
		nodeType *current = first->next;
		nodeType *trailCurrent = first;
		while (current != last)
		{
			trailCurrent = current;
			current = current->next;
		}
		delete current;
		trailCurrent->next = NULL;
		last = trailCurrent;
		length--;
	}
}

// Alternative implementation to remove the last element
void linkedListType::removeLast2()
{
	if (length == 0)
		cout << "ERROR: EMPTY LIST\n";
	else if (length == 1)
	{
		delete first;
		last = first = NULL;
		length--;
	}
	else
	{
		nodeType *current = first;
		while (current->next != last)
			current = current->next;

		delete last;
		current->next = NULL;
		last = current;
		length--;
	}
}

// Remove element at a specific index
void linkedListType::removeAt(int loc)
{
	if (loc < 0 || loc >= length)
		cout << "ERROR: Out of range\n";
	else
	{
		nodeType *current, *trailCurrent;
		if (loc == 0)
		{
			current = first;
			first = first->next;
			delete current;
			length--;
			if (length == 0)
				last = NULL;
		}
		else
		{
			current = first->next;
			trailCurrent = first;
			for (int i = 1; i < loc; i++)
			{
				trailCurrent = current;
				current = current->next;
			}

			trailCurrent->next = current->next;
			if (last == current)
				last = trailCurrent;
			delete current;
			length--;
		}
	}
}

// Remove first occurrence of a specific value
void linkedListType::remove(int item)
{
	if (isEmpty())
	{
		cout << "Can not remove from empty list\n";
		return;
	}

	nodeType *current, *trailCurrent;
	if (first->info == item)
	{
		current = first;
		first = first->next;
		delete current;
		length--;
		if (length == 0)
			last = NULL;
	}
	else
	{
		current = first->next;
		trailCurrent = first;
		while (current != NULL)
		{
			if (current->info == item)
				break;
			trailCurrent = current;
			current = current->next;
		}

		if (current == NULL)
			cout << "The item is not there\n";
		else
		{
			trailCurrent->next = current->next;
			if (last == current)
				last = trailCurrent;
			delete current;
			length--;
		}
	}
}

// Linear search for an element and return its index
int linkedListType::seqSearch(int item)
{
	nodeType *current = first;
	int loc = 0;
	while (current != NULL)
	{
		if (current->info == item)
			return loc;
		current = current->next;
		loc++;
	}
	return -1;
}

// Remove all odd numbers and return sum of remaining even numbers
int linkedListType::removeOddSumEven()
{
	int sum = first->info;
	nodeType *current = first->next;
	nodeType *trailCurrent = first;

	while (current != NULL)
	{
		if (current->info % 2 == 0)
		{
			sum += current->info;
			trailCurrent = current;
			current = current->next;
		}
		else
		{
			trailCurrent->next = current->next;
			delete current;
			length--;
			current = trailCurrent->next;
		}
	}
	return sum;
}

// Reverse the linked list in-place
void linkedListType::reverse()
{
	nodeType *prev = NULL;
	nodeType *curr = first;
	nodeType *next = NULL;

	last = first;
	while (curr != NULL)
	{
		next = curr->next;
		curr->next = prev;
		prev = curr;
		curr = next;
	}
	first = prev;
}

// Print all elements
void linkedListType::print()
{
	nodeType *current = first;
	while (current != NULL)
	{
		cout << current->info << " -> ";
		current = current->next;
	}
	cout << "NULL\n";
}

// Free all allocated nodes
void linkedListType::clearList()
{
	nodeType *current;
	while (first != NULL)
	{
		current = first;
		first = first->next;
		delete current;
	}
	last = NULL;
	length = 0;
}

// Destructor: Clean up list memory
linkedListType::~linkedListType()
{
	clearList();
}

int main()
{
	linkedListType l1;
	l1.insertAt(0, 10);
	l1.insertAt(1, 15);
	l1.insertAt(2, 20);
	l1.insertAt(3, 25);
	
	cout << "List contents:\n";
	l1.print();

	return 0;
}
