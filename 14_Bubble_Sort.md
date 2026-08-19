// Objective: Implementation of Bubble Sort algorithm (Iterative and Recursive) with early-exit optimization.
// Logic: Repeatedly compare adjacent elements and swap them if they are in the wrong order.
// Time Complexity: O(n) Best case (when already sorted) | O(n^2) Average & Worst case
// Space Complexity: O(1) for iterative | O(n) call stack for recursive

#include <iostream>
#include <algorithm>

using namespace std;

// Iterative Bubble Sort with optimization flag
void bubbleSort(int arr[], int n)
{
	bool swapped;
	int comparisonCount = 0;

	for (int i = 0; i < n - 1; i++)
	{
		swapped = false;

		for (int j = 0; j < n - i - 1; j++)
		{
			if (arr[j] > arr[j + 1])
			{
				swap(arr[j], arr[j + 1]);
				swapped = true;
			}
			comparisonCount++;
		}

		// If no two elements were swapped, array is already sorted
		if (!swapped)
			break;
	}

	cout << "# of comparisons: " << comparisonCount << endl;
}

// Recursive Bubble Sort
void bubbleSortRec(int arr[], int n)
{
	// Base case
	if (n == 1)
		return;

	// One pass of bubble sort (moves the largest element to the end)
	for (int i = 0; i < n - 1; i++)
	{
		if (arr[i] > arr[i + 1])
			swap(arr[i], arr[i + 1]);
	}

	// Recursively sort remaining n-1 elements
	bubbleSortRec(arr, n - 1);
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
	int arr[] = { 30, 20, 40, 5, 60, 2 };
	int n = sizeof(arr) / sizeof(arr[0]);

	bubbleSort(arr, n);
	printArray(arr, n);

	return 0;
}
