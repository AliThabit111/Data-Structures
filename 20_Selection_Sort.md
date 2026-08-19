// Objective: Implementation of Selection Sort algorithm (Iterative and Recursive).
// Logic: Repeatedly find the minimum/maximum element from the unsorted part and put it at the beginning.
// Time Complexity: O(n^2) in all cases (Best, Average, Worst)
// Space Complexity: O(1) auxiliary space for iterative | O(n) call stack for recursive

#include <iostream>
#include <algorithm>

using namespace std;

// Iterative Selection Sort (Descending Order: > or Ascending Order: <)
void selectionSort(int arr[], int n)
{
	int minIdx;
	for (int i = 0; i < n - 1; i++)
	{	
		minIdx = i;

		for (int j = i + 1; j < n; j++)
		{
			if (arr[j] > arr[minIdx]) // Change '>' to '<' for ascending order
				minIdx = j;
		}

		if (minIdx != i)
			swap(arr[minIdx], arr[i]);
	}
}

// Recursive helper to find minimum element index
int minIndex(int a[], int i, int j)
{
	if (i == j)
		return i;

	int k = minIndex(a, i + 1, j);

	return (a[i] < a[k]) ? i : k;
}

// Recursive Selection Sort
void recurSelectionSort(int a[], int n, int index = 0)
{
	if (index == n)
		return;

	int k = minIndex(a, index, n - 1);

	if (k != index)
		swap(a[k], a[index]);

	recurSelectionSort(a, n, index + 1);
}

// Print array elements
void print(int arr[], int size)
{
	for (int i = 0; i < size; i++)
		cout << arr[i] << " ";
	cout << endl;
}

int main()
{
	int arr[] = { -60, 0, 50, 30, 10, 20 };
	int n = sizeof(arr) / sizeof(arr[0]);

	selectionSort(arr, n);
	cout << "Array After Selection Sort:\n";
	print(arr, n);

	return 0;
}
