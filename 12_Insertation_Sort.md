// Objective: Implementation of Insertion Sort algorithm (Iterative and Recursive).
// Logic: Build a sorted sub-array one element at a time by shifting larger elements.
// Time Complexity: O(n) Best case (already sorted) | O(n^2) Average & Worst case
// Space Complexity: O(1) for iterative | O(n) call stack for recursive

#include<iostream>
using namespace std;

// Iterative Insertion Sort (Descending Order: > or Ascending: <)
void insertionSort(int arr[], int n)
{
	int key, j;                
	for (int i = 1; i < n; i++)
	{
		key = arr[i];
		j = i - 1;

		// Shift elements to make space for key
		while (j >= 0 && arr[j] < key)
		{
			arr[j + 1] = arr[j];
			j = j - 1;
		}
		arr[j + 1] = key;
	}
}

// Recursive Insertion Sort (Ascending Order)
void insertionSortRecursive(int arr[], int n)
{
	// Base case: if array size is 1 or smaller
	if (n <= 1)
		return;

	// Sort first n-1 elements recursively
	insertionSortRecursive(arr, n - 1);

	int last = arr[n - 1];
	int j = n - 2;

	// Shift elements greater than last
	while (j >= 0 && arr[j] > last)
	{
		arr[j + 1] = arr[j];
		j--;
	}
	arr[j + 1] = last;
}

// Print elements of the array
void printArray(int arr[], int n)
{
	for (int i = 0; i < n; i++)
		cout << arr[i] << " ";
	cout << endl;
}

int main()
{
	int arr[] = { 80, 90, 60, 30, 50, 70, 40 };
	int n = sizeof(arr) / sizeof(arr[0]);

	insertionSort(arr, n);
	printArray(arr, n);

	return 0;
}
