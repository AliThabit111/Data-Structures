// Objective: Implementation of an Array-based List (Dynamic Array List).
// Operations: insertAt, insertEnd, insertNoDuplicate, removeAt, remove, retrieveAt, replaceAt, seqSearch, print.
// Time Complexity: O(1) for insertEnd, retrieveAt, replaceAt | O(n) for insertAt, removeAt, seqSearch, print
// Space Complexity: O(maxSize) dynamic array allocation

#include <iostream>
#include <cassert>

using namespace std;

class arrayListType
{
public:
	arrayListType(int size = 100);
	arrayListType(const arrayListType& otherList); // Copy constructor	
	~arrayListType();                             // Destructor

	bool isEmpty();
	bool isFull();
	int listSize();
	int maxListSize();
	void print();
	bool isItemAtEqual(int loc, int item);
	void insertAt(int loc, int item);
	void insertEnd(int item);
	void removeAt(int loc);
	void retrieveAt(int loc, int& item);
	void replaceAt(int loc, int item);
	void clearList();
	int seqSearch(int item);
	void insertNoDuplicate(int item);
	void remove(int item);

private:
	int *list;     // Dynamic array to hold the list elements
	int length;    // Current number of elements
	int maxSize;   // Maximum capacity of the list
};

// Constructor
arrayListType::arrayListType(int size)
{
	if (size <= 0)
	{
		cout << "Wrong Size\n";
		maxSize = 100;
	}
	else
		maxSize = size;

	length = 0;
	list = new int[maxSize];
	assert(list != NULL);
}

// Copy Constructor (Deep Copy)
arrayListType::arrayListType(const arrayListType& otherList)
{
	maxSize = otherList.maxSize;
	length = otherList.length;
	list = new int[maxSize];
	assert(list != NULL);

	for (int j = 0; j < length; j++)
		list[j] = otherList.list[j];
}

// Destructor: Free allocated memory
arrayListType::~arrayListType()
{
	delete[] list;
}

bool arrayListType::isEmpty()
{
	return (length == 0);
}

bool arrayListType::isFull()
{
	return (length == maxSize);
}

int arrayListType::listSize()
{
	return length;
}

int arrayListType::maxListSize()
{
	return maxSize;
}

// Print elements of the list
void arrayListType::print()
{
	for (int i = 0; i < length; i++)
		cout << list[i] << " ";
	cout << endl;
}

// Check if item at given index equals the specified value
bool arrayListType::isItemAtEqual(int loc, int item)
{
	if (loc < 0 || loc >= length)
		return false;
	else
		return (list[loc] == item);
}

// Insert item at specific index by shifting elements right
void arrayListType::insertAt(int loc, int item)
{
	if (isFull())
		cout << "The List is Full\n";
	else if (loc < 0 || loc > length)
		cout << "Out of Range\n";
	else
	{
		for (int i = length; i > loc; i--)
			list[i] = list[i - 1]; // Shift right
		
		list[loc] = item;
		length++;
	}
}

// Insert item at the end of the list
void arrayListType::insertEnd(int item)
{
	if (isFull())
		cout << "The List is Full\n";
	else
		list[length++] = item;
}

// Retrieve element at index
void arrayListType::retrieveAt(int loc, int& item)
{
	if (loc < 0 || loc >= length)
		cout << "Out of Range\n";
	else
		item = list[loc];
}

// Replace element at index
void arrayListType::replaceAt(int loc, int item)
{
	if (loc < 0 || loc >= length)
		cout << "Out of Range\n";
	else
		list[loc] = item;
}

// Reset list
void arrayListType::clearList()
{
	length = 0;
}

// Linear search for an item
int arrayListType::seqSearch(int item)
{
	for (int loc = 0; loc < length; loc++)
		if (list[loc] == item)
			return loc;
	return -1;
}

// Insert item only if it does not already exist
void arrayListType::insertNoDuplicate(int item)
{
	if (isFull())
		cout << "The List is Full\n";
	else
	{
		int flag = seqSearch(item);
		if (flag == -1)
			list[length++] = item;
		else
			cout << "No duplicates are allowed.\n";
	}			
}

// Remove first occurrence of item by value
void arrayListType::remove(int item)
{
	int loc = seqSearch(item);
	if (loc == -1)
		cout << "The item to be deleted is not in the list\n";
	else
		removeAt(loc);
}

// Remove item at index by shifting elements left
void arrayListType::removeAt(int loc)
{
	if (loc < 0 || loc >= length)
		cout << "The location of the item to be removed is out of range.\n";
	else
	{
		for (int i = loc; i < length - 1; i++)
			list[i] = list[i + 1]; // Shift left

		length--;
	}
}

int main()
{
	arrayListType lst1;

	for (int i = 0; i < 20; i++)
		lst1.insertAt(i, i * i);

	lst1.print();
	
	int x;
	lst1.retrieveAt(10, x);
	cout << "Value at index 10: " << x << endl;

	arrayListType lst2(lst1); // Copy constructor
	lst2.print();

	return 0;
}
