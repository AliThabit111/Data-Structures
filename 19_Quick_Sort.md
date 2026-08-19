// Objective: Implementation of Quick Sort algorithm using Divide and Conquer with two partition approaches.
// Logic: Select a pivot, partition elements smaller to the left and larger to the right, then sort recursively.
// Time Complexity: O(n log n) Best & Average case | O(n^2) Worst case (sorted/reversed array with poor pivot)
// Space Complexity: O(log n) recursion call stack

#include <iostream>
#include <algorithm>

using namespace std;

// Hoare-like partition scheme
int partition1(int arr[], int l, int h)
{
	int p = arr[l];
	int i = l;
	int j = h;

	while (i < j)
	{
		do
		{
			i++;
		} while (arr[i] <= p);

		do
		{
			j--;
		} while (arr[j] > p);

		if (i < j)
			swap(arr[i], arr[j]);
	}

	swap(arr[l], arr[j]);
	return j;
}

// QuickSort using partition1
void quickSort1(int arr[], int l, int h)
{
	if (l < h) {
		int piv = partition1(arr, l, h);
		quickSort1(arr, l, piv);
		quickSort1(arr, piv + 1, h);
	}
}

// Two-way pointer partition with dynamic pivot tracking
int partition2(int arr[], int iBegin, int jEnd)
{
	int i = iBegin;
	int j = jEnd;
	int pivLoc = i;

	while (true)
	{
		// Move right pointer leftwards
		while (arr[pivLoc] <= arr[j] && pivLoc != j)
		{
			j--;
		}
		if (pivLoc == j)
			break;
		else if (arr[pivLoc] > arr[j])
		{
			swap(arr[j], arr[pivLoc]);
			pivLoc = j;
		}

		// Move left pointer rightwards
		while (arr[pivLoc] >= arr[i] && pivLoc != i)
		{
			i++;
		}
		if (pivLoc == i)
			break;
		else if (arr[pivLoc] < arr[i])
		{
			swap(arr[i], arr[pivLoc]);
			pivLoc = i;
		}
	}
	return pivLoc;
}

// QuickSort using partition2
void quickSort2(int arr[], int l, int h)
{
	if (l < h) {
		int piv = partition2(arr, l, h);
		quickSort2(arr, l, piv - 1);
		quickSort2(arr, piv + 1, h);
	}
}

// Print array elements
void printArray(int arr[], int n)
{
	for (int i = 0; i < n; i++)
	{
		cout << arr[i] << " ";
	}
	cout << endl;
}

int main()
{
	int arr[] = { 2, -1, 4, 7, 0 };
	int n = sizeof(arr) / sizeof(arr[0]);

	quickSort2(arr, 0, n - 1);
	printArray(arr, n);

	return 0;
}
