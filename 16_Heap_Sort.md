// Objective: Implementation of Heap Sort algorithm using a Max-Heap.
// Logic: Build a max-heap from the array, repeatedly extract the root (maximum) to the end, and restore the heap property.
// Time Complexity: O(n log n) in all cases (Best, Average, Worst)
// Space Complexity: O(log n) recursion call stack | O(1) auxiliary space

#include <iostream>
#include <algorithm>

using namespace std;

// Maintain the max-heap property for subtree rooted at index i
void heapify(int arr[], int n, int i)
{
	int l = 2 * i + 1; // Left child index
	int r = 2 * i + 2; // Right child index
	int max = i;       // Initialize largest as root

	// Check if left child is larger than root
	if (l < n && arr[l] > arr[max])
		max = l;

	// Check if right child is larger than current largest
	if (r < n && arr[r] > arr[max])
		max = r;

	// If largest is not root, swap and continue heapifying affected subtree
	if (max != i) {
		swap(arr[i], arr[max]);
		heapify(arr, n, max);
	}
}

// Build a max-heap from an unsorted array
void buildHeap(int arr[], int n)
{
	// Start from the last non-leaf node down to the root
	for (int i = n / 2 - 1; i >= 0; i--)
		heapify(arr, n, i);
}

// Main function to perform heap sort
void heapSort(int arr[], int n)
{
	buildHeap(arr, n);

	// Extract elements from heap one by one
	for (int i = n - 1; i >= 0; i--)
	{
		swap(arr[0], arr[i]); // Move current root to end
		heapify(arr, i, 0);   // Call heapify on the reduced heap
	}
}

// Print elements of the array
void print(int arr[], int n)
{
	for (int i = 0; i < n; i++)
	{
		cout << arr[i] << " ";
	}
	cout << endl;
}

int main()
{
	int arr[] = { 90, 10, 40, 70, 5 };
	int n = sizeof(arr) / sizeof(arr[0]);

	heapSort(arr, n);
	print(arr, n);

	return 0;
}
