# Array-lovebabbar
## 1.Write a program to reverse an array or string?
### Input  : arr[] = {1, 2, 3}
### Output : arr[] = {3, 2, 1}
#### #include<bits/stdc++.h>
#### using namespace std;
#### typedef long long int ll;
#### #define fast    ios_base::sync_with_stdio(false); cin.tie(NULL); cout.tie(NULL);
#### int main()
#### {
####   vector<int> v1;
####   int n;
####   cin>>n;
####  for(int i=0;i<n;i++)
####  {
####   int x;
####    cin>>x;
####    v1.push_back(x);
####  }
####   reverse(v1.begin(),v1.end());
####   for(int i=0;i<n;i++)
####     cout<<v1[i]<<" ";
####   return 0;
#### }
                       
 
## 2.Maximum and minimum of an array using minimum number of comparisons?
#### We can also use stl for finding maximum amd minimum element in c++.We can also find from using sorting method.
#### for return multiple values ,so we will use structure.
  
#### #include<iostream>
#### using namespace std;


#### struct Pair
#### {
#### 	int min;
#### 	int max;
#### };

#### struct Pair getMinMax(int arr[], int n)
#### {
#### 	struct Pair minmax;	
#### 	int i;
	

####	if (n == 1)
####	{
####		minmax.max = arr[0];
####		minmax.min = arr[0];	
####		return minmax;
####	}
	
####	// If there are more than one elements,
####	// then initialize min and max
#### 	if (arr[0] > arr[1])
####	{
####		minmax.max = arr[0];
####		minmax.min = arr[1];
####	}
####	else
####	{
####		minmax.max = arr[1];
####		minmax.min = arr[0];
####	}
	
####	for(i = 2; i < n; i++)
####	{
####		if (arr[i] > minmax.max)	
####			minmax.max = arr[i];
			
####		else if (arr[i] < minmax.min)	
####			minmax.min = arr[i];
####	}
####	return minmax;
#### }


#### int main()
#### {
####	int arr[] = { 1000, 11, 445,
####				1, 330, 3000 };
#### 	int arr_size = 6;
	
####	struct Pair minmax = getMinMax(arr, arr_size);
	
####	cout << "Minimum element is "
####		<< minmax.min << endl;
####	cout << "Maximum element is "
####		<< minmax.max;
		
####	return 0;
#### }

 ## 3.Given an array arr[] and an integer K where K is smaller than size of array, the task is to find the Kth smallest element in the given array. It is given that all array
 ## elements are distinct.
  #### We can definitely use sorting for finding the kth smallest and largest .
  #### a.Using Set 
 #### #include <bits/stdc++.h>
####     using namespace std;
  
####  int main()
#### {
  
 ####   int arr[] = { 12, 3, 5, 7, 19 };
 ####   int n = sizeof(arr) / sizeof(arr[0]);
 ####   int k = 4;
  
 ####   set<int> s(arr, arr + n);
 ####   set<int>::iterator itr
####        = s.begin(); // s.begin() returns a pointer to first
####                     // element in the set
####    advance(itr, k - 1); // itr points to kth element in set
  
####    cout << *itr << "\n";
  
####    return 0;
#### }
  
  #####Time complexity in best case is O(logn) and in worst case is O(n)
  
  #### b.Using Max Heap
 ####// A C++ program to find k'th smallest element using max heap
#### #include <iostream>
#### using namespace std;

#### // Prototype of a utility function to swap two integers
#### void swap(int* x, int* y);

#### // A class for Max Heap
#### class MaxHeap {
####	int* harr; // pointer to array of elements in heap
#### 	int capacity; // maximum possible size of max heap
####	int heap_size; // Current number of elements in max heap
#### public:
#### 	MaxHeap(int a[], int size); // Constructor
#### 	void maxHeapify(int i); // To maxHeapify subtree rooted with index i
#### 	int parent(int i) { return (i - 1) / 2; }
####	int left(int i) { return (2 * i + 1); }
#### 	int right(int i) { return (2 * i + 2); }

####	int extractMax(); // extracts root (maximum) element
####	int getMax() { return harr[0]; } // Returns maximum

####	// to replace root with new node x and heapify() new root
####	void replaceMax(int x)
####	{
####		harr[0] = x;
####		maxHeapify(0);
####	}
#### };

#### MaxHeap::MaxHeap(int a[], int size)
#### {
####	heap_size = size;
####	harr = a; // store address of array
####	int i = (heap_size - 1) / 2;
####	while (i >= 0) {
####		maxHeapify(i);
####		i--;
####	}
####}

#### // Method to remove maximum element (or root) from max heap
#### int MaxHeap::extractMax()
#### {
####	if (heap_size == 0)
####		return INT_MAX;

####	// Store the maximum vakue.
####	int root = harr[0];

####	// If there are more than 1 items, move the last item to root
####	// and call heapify.
####	if (heap_size > 1) {
####		harr[0] = harr[heap_size - 1];
####		maxHeapify(0);
####	}
####	heap_size--;

####	return root;
#### }

#### // A recursive method to heapify a subtree with root at given index
#### // This method assumes that the subtrees are already heapified
#### void MaxHeap::maxHeapify(int i)
#### {
####	int l = left(i);
####	int r = right(i);
####	int largest = i;
####	if (l < heap_size && harr[l] > harr[i])
####		largest = l;
####	if (r < heap_size && harr[r] > harr[largest])
####		largest = r;
####	if (largest != i) {
####		swap(&harr[i], &harr[largest]);
####		maxHeapify(largest);
####	}
#### }

#### // A utility function to swap two elements
#### void swap(int* x, int* y)
#### {
####	int temp = *x;
####	*x = *y;
####	*y = temp;
####}

#### // Function to return k'th largest element in a given array
#### int kthSmallest(int arr[], int n, int k)
#### {
####	// Build a heap of first k elements: O(k) time
####	MaxHeap mh(arr, k);

####	// Process remaining n-k elements. If current element is
####	// smaller than root, replace root with current element
####	for (int i = k; i < n; i++)
####		if (arr[i] < mh.getMax())
####			mh.replaceMax(arr[i]);

####	// Return root
####	return mh.getMax();
#### }

#### // Driver program to test above methods
#### int main()
#### {
####	int arr[] = { 12, 3, 5, 7, 19 };
####	int n = sizeof(arr) / sizeof(arr[0]), k = 4;
####	cout << "K'th smallest element is " << kthSmallest(arr, n, k);
####	return 0;
#### }


#### 4.Given an array of size N containing only 0s, 1s, and 2s; sort the array in ascending order.
	##### 1.Using sort() method
	##### 2.number of times 0's,1's,2's 
##### // C++ implementation of the approach
##### #include <bits/stdc++.h>
##### using namespace std;

##### // Utility function to print the contents of an array
##### void printArr(int arr[], int n)
##### {
##### 	for (int i = 0; i < n; i++)
##### 		cout << arr[i] << " ";
##### }

##### // Function to sort the array of 0s, 1s and 2s
##### void sortArr(int arr[], int n)
##### {
##### 	int i, cnt0 = 0, cnt1 = 0, cnt2 = 0;

#####	// Count the number of 0s, 1s and 2s in the array
##### 	for (i = 0; i < n; i++) {
##### 		switch (arr[i]) {
##### 		case 0:
##### 			cnt0++;
##### 			break;
##### 		case 1:
##### 			cnt1++;
##### 			break;
##### 		case 2:
##### 			cnt2++;
##### 			break;
##### 		}
##### 	}

##### 	// Update the array
##### 	i = 0;

##### // Store all the 0s in the beginning
##### 	while (cnt0 > 0) {
##### 		arr[i++] = 0;
##### 		cnt0--;
##### 	}

##### 	// Then all the 1s
##### while (cnt1 > 0) {
##### 		arr[i++] = 1;
##### 		cnt1--;
##### 	}

#####	// Finally all the 2s
##### 	while (cnt2 > 0) {
##### 		arr[i++] = 2;
##### 		cnt2--;
##### 	}

##### 	// Print the sorted array
##### 	printArr(arr, n);
##### }

##### // Driver code
##### int main()
##### {
#####	int arr[] = { 0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1 };
#####	int n = sizeof(arr) / sizeof(int);

#####	sortArr(arr, n);

 ##### return 0;
##### }

#### 5.Kadane Algorithm
	#####// C++ program to print largest contiguous array sum
##### #include<iostream>
##### #include<climits>
##### using namespace std;
 
##### int maxSubArraySum(int a[], int size)
##### {
#####     int max_so_far = INT_MIN, max_ending_here = 0;
##### 
#####     for (int i = 0; i < size; i++)
#####     {
#####         max_ending_here = max_ending_here + a[i];
#####         if (max_so_far < max_ending_here)
#####             max_so_far = max_ending_here;
 
#####         if (max_ending_here < 0)
#####             max_ending_here = 0;
#####     }
#####     return max_so_far;
##### }
 
##### /*Driver program to test maxSubArraySum*/
##### int main()
##### {
#####     int a[] = {-2, -3, 4, -1, -2, 1, 5, -3};
#####     int n = sizeof(a)/sizeof(a[0]);
#####     int max_sum = maxSubArraySum(a, n);
#####    cout << "Maximum contiguous sum is " << max_sum;
#####     return 0;
### 6.Count Minimum Number of Jumps to reach End
Input: arr[] = {1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9}
Output: 3 (1-> 3 -> 9 -> 9)
Explanation: Jump from 1st element 
to 2nd element as there is only 1 step, 
now there are three options 5, 8 or 9. 
If 8 or 9 is chosen then the end node 9 
can be reached. So 3 jumps are made.
	
Method 3: Dynamic Programming. 
In this method, we build jumps[] array from right to left such that jumps[i] indicates the minimum number of jumps needed to reach arr[n-1] from arr[i]. Finally, we return jumps[0]. 
	
// C++ program to find Minimum
// number of jumps to reach end
#include <bits/stdc++.h>
using namespace std;

// Returns Minimum number of
// jumps to reach end
int minJumps(int arr[], int n)
{
	// jumps[0] will hold the result
	int* jumps = new int[n];
	int min;

	// Minimum number of jumps needed
	// to reach last element from last
	// elements itself is always 0
	jumps[n - 1] = 0;

	// Start from the second element,
	// move from right to left and
	// construct the jumps[] array where
	// jumps[i] represents minimum number
	// of jumps needed to reach
	// arr[m-1] from arr[i]
	for (int i = n - 2; i >= 0; i--) {
		// If arr[i] is 0 then arr[n-1]
		// can't be reached from here
		if (arr[i] == 0)
			jumps[i] = INT_MAX;

		// If we can directly reach to
		// the end point from here then
		// jumps[i] is 1
		else if (arr[i] >= n - i - 1)
			jumps[i] = 1;

		// Otherwise, to find out the minimum
		// number of jumps needed to reach
		// arr[n-1], check all the points
		// reachable from here and jumps[]
		// value for those points
		else {
			// initialize min value
			min = INT_MAX;

			// following loop checks with all
			// reachable points and takes
			// the minimum
			for (int j = i + 1; j < n && j <= arr[i] + i; j++) {
				if (min > jumps[j])
					min = jumps[j];
			}

			// Handle overflow
			if (min != INT_MAX)
				jumps[i] = min + 1;
			else
				jumps[i] = min; // or INT_MAX
		}
	}

	return jumps[0];
}

// Driver program to test above function
int main()
{
	int arr[] = { 1, 3, 6, 1, 0, 9 };
	int size = sizeof(arr) / sizeof(int);
	cout << "Minimum number of jumps to reach"
		<< " end is " << minJumps(arr, size);
	return 0;
}
Time Complexity :O(n^2)
So,If you want time complexity in O(n) times
	// C++ program to count Minimum number
// of jumps to reach end
#include <bits/stdc++.h>
using namespace std;

int max(int x, int y)
{
	return (x > y) ? x : y;
}

// Returns minimum number of jumps
// to reach arr[n-1] from arr[0]
int minJumps(int arr[], int n)
{

	// The number of jumps needed to
	// reach the starting index is 0
	if (n <= 1)
		return 0;

	// Return -1 if not possible to jump
	if (arr[0] == 0)
		return -1;

	// initialization
	// stores all time the maximal
	// reachable index in the array.
	int maxReach = arr[0];

	// stores the number of steps
	// we can still take
	int step = arr[0];

	// stores the number of jumps
	// necessary to reach that maximal
	// reachable position.
	int jump = 1;

	// Start traversing array
	int i = 1;
	for (i = 1; i < n; i++) {
		// Check if we have reached the end of the array
		if (i == n - 1)
			return jump;

		// updating maxReach
		maxReach = max(maxReach, i + arr[i]);

		// we use a step to get to the current index
		step--;

		// If no further steps left
		if (step == 0) {
			// we must have used a jump
			jump++;

			// Check if the current index/position or lesser index
			// is the maximum reach point from the previous indexes
			if (i >= maxReach)
				return -1;

			// re-initialize the steps to the amount
			// of steps to reach maxReach from position i.
			step = maxReach - i;
		}
	}

	return -1;
}

// Driver program to test above function
int main()
{
	int arr[] = { 1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9 };
	int size = sizeof(arr) / sizeof(int);

	// Calling the minJumps function
	cout << ("Minimum number of jumps to reach end is %d ",
			minJumps(arr, size));
	return 0;
}
// This code is contributed by


	
