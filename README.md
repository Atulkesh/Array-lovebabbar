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
