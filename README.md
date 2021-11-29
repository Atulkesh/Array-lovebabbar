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
####};

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
####}

####// A recursive method to heapify a subtree with root at given index
####// This method assumes that the subtrees are already heapified
####void MaxHeap::maxHeapify(int i)
####{
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
####}

#### // A utility function to swap two elements
####void swap(int* x, int* y)
####{
####	int temp = *x;
####	*x = *y;
####	*y = temp;
####}

####// Function to return k'th largest element in a given array
####int kthSmallest(int arr[], int n, int k)
####{
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
####int main()
#### {
####	int arr[] = { 12, 3, 5, 7, 19 };
####	int n = sizeof(arr) / sizeof(arr[0]), k = 4;
####	cout << "K'th smallest element is " << kthSmallest(arr, n, k);
####	return 0;
####}


