// Objective: Search for an element sequentially in an unsorted/sorted array using Linear Search.
// Logic: Iterate through the array element by element until a match is found or end is reached.
// Time Complexity: O(1) Best case (first element) | O(n) Average & Worst case
// Space Complexity: O(1) auxiliary space

#include <iostream>
using namespace std;

// Sequential search for key in array of size n
int linearSearch(int arr[], int n, int key)
{
	for (int i = 0; i < n; i++)
	{
		if (arr[i] == key)
			return i; // Return index where key was found
	}
	return -1; // Return -1 if not found
}

int main()
{
	int arr[] = { 90, 10, 40, 70, 5 };
	int n = sizeof(arr) / sizeof(arr[0]);

	int num;
	cout << "Enter an Integer: ";
	cin >> num;

	int result = linearSearch(arr, n, num);
	if (result == -1)
		cout << "The Number: (" << num << ") Was Not Found." << endl;
	else
		cout << "The Number: (" << arr[result] << ") Was Found At Index: (" << result << ")" << endl;

	return 0;
}
