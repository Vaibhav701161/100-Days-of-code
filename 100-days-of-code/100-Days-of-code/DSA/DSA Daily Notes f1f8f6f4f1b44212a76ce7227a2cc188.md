# DSA Daily Notes

- DAY-1 (11TH JULY , 2024)
    
    ### SORTING TECHNIQUES PART 1:
    
    1. SELECTION SORT:
    - As the name suggests , we will select the minimums in the array .
    - Select the minimums and swap. that’s what the  algo is all about.
    - So, let use suppose this is an array :
    
    [13,46,24,52,20,9]  , so we will swap 9 and 13 as 9 is the minimum and 13 is at the zeroth index →   [9,46,24,52,20,13].
    
    - We will repeat this action until the array gets sorted in ascending order.
    - So, if we observe carefully , an array with 6 elements will take 5 steps to get sorted!
    - **OBSERVATIONS AND PSUEDOCODE**
    1. In the entire array , figure out the minimum, and whichever index the minimum be at ,  swap it with the 0th index.
    2. In the next step , I went from the index 1 to 5 ,  found the smallest and swapped with the element at the 1st index. (The swapping happened with 1 and the index of the minimum element!)
    3. Now, carefully observing the pattern ,  the first swap happened at index 0 [0 -  n-1].
    4. The second swap happened at index 1 [1 - n-1].
    5. This continues until the array is completely sorted.
    6. **MOST IMP OBSERVATION :** 
    By the time `i` reaches `n-2`, the array is already sorted because the last element naturally falls into place.
    7. Logic inside the for loop : whenever i is 0; I find the minimum from 0 to      n-1. Then from 1 to n-1 and so on.
    8. Logic inside the second for loop: when we start sorting out we consider that our minimum appears at index i. 
    9. Logic of if statement : when we are iterating element by element , we check if the element is smaller than the element at the jth index or not.
    10. If the element at the jth index is smaller , assign the min to jth element.
    
    ```cpp
    for(i=0,i<= n-2;i++){
    for (j=i; j<n-1;j++){
      if (arr[j] < arr[min]){
         min = j;
      }
      
    }
    swap(arr[min],arr[i]);
    }
    ```
    
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    void selection_sort(int arr[],int n){
    for(int i =0;i<=n;i++){
    int mini =i;
    for int j = i;j<n-1;j++{
    if(arr[i] < arr[mini]){
    mini = j;
    }
    }
    int temp = arr[mini];
    arr[mini] = arr[i];
    arr[i] = temp;
    }
    }
    
    int main() {
        int n;
        cin >> n; // Read the number of elements in the array
        int arr[100]; // Declare an array of size 100 (or any large enough size)
        for (int i = 0; i < n; i++) { // Loop to read the array elements
            cin >> arr[i]; // Read each element of the array
        }
        selection_sort(arr, n); // Call the selection_sort function to sort the array
        for (int i = 0; i < n; i++) { // Loop to print the sorted array elements
            cout << arr[i] << " "; // Print each element followed by a space
        }
        return 0; 
    }
    
    ```
    
    1. **BUBBLE SORT:**
    - In bubble sort,  we push the max to the last by adjacent swaps.
    - So, after the first step, the last element in the array is sorted. Now, we run the algorithm again !
    - In the first step we went from 0- n-1, next time form         0 - n-2, then from 0- n-3 and so on till 0 to 1.
    - IMP : if we try to access an index which is not present , it will throw a runtime error.
    
    ```cpp
    for (i = n-1 ;i>=1; i--){
    for(j = 0;j<=i-1;j++){
          if(arr[j]> arr[j+1]){
             swap;
          }
    }
    }
    ```
    
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    
    // Bubble sort function
    void bubble_sort(int arr[], int n) {
        for (int i = 0; i < n - 1; i++) { // Outer loop for the number of passes
            for (int j = 0; j < n - i - 1; j++) { // Inner loop for each pass
                if (arr[j] > arr[j + 1]) { // If the current element is greater than the next element
                    // Swap the elements
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }
    
    int main() {
        int n;
        cin >> n; // Read the number of elements in the array
        int arr[100]; // Declare an array of size 100 (or any large enough size)
        for (int i = 0; i < n; i++) { // Loop to read the array elements
            cin >> arr[i]; // Read each element of the array
        }
        bubble_sort(arr, n); // Call the bubble_sort function to sort the array
        for (int i = 0; i < n; i++) { // Loop to print the sorted array elements
            cout << arr[i] << " "; // Print each element followed by a space
        }
        return 0; 
    }
    
    ```
    
- DAY-2 (12TH JULY, 2024)
    1. **Insertion Sort**
        - Inserts an element from unsorted array to it’s correct position in sorted array.
        - You move towards left, compare adjacent elements and swap in ascending order.
        - For every guy, I am just looking at left and see are you greater? → swap , are you greater? → swap and so on till it is possible on the left!
    
    ```cpp
    for (i = 1;i<= n; i++){
    j=i;
    while(j<0 && a[j-1] > a[j]){
       swap(a[j-1], a[j]);
       j--;
    }
    }
    ```
    
    ```cpp
    #include <iostream.
    usingnamespace std;
    
    int main(){
     int n;
     cin n;
     
     int arr[n];
     for(int i = 0; i<n;i++){
     cin arr[i];
     }
     
     for (int i = 1 ; i<n;i++){
         int current = arr[i];
         int j = i-1;
           while(arr[j]> current && j>=0){
                 arr[j+1] = arr[j];
                 j--;
           }
           arr[j+1] = current;
     }
      for (int i = 0 ; i<n;i++){
          cout << arr[i]<<"  ";
      }
    }
    ```
    
    1. **Merge Sort:**
    - We first of all find the mid of our array, and divide the array into two.
    - We again call the merge sort algorithm of the obtained two arrays.
    
    ```cpp
    #include<iostream>
    using namespace std;
     void merge(arr[],int l ,int mid , int r){
        int n1 = mid- l + 1;
        int n2 = r - mid;
        
        int a[n1];
        int b[n2]; // temp arrays
        
        for (int i=0 ; i<n1;i++){
           a[i] = arr[l+i];
        }
        
        for (int i=0 ; i<n2;i++){
           a[i] = arr[mid+1+i];
        }
        
        int i =0;
        int j = 0;
        int k = l;
        while(i<n1 && j<n2){
          if(a[i]< b[j]){
             arr[k] = arr[i];
             k++; i++;
           } else{
               arr[k] = b[j];
               k++;j++;
           }
        }
        while (i<n1){
           arr[k] = arr[i];
             k++; i++;
        }
        while (j<n2){
        arr[k] = b[j];
               k++;j++;
        }
     }
    
    void mergeSort(int arr[], int l,int r){
    if (l,r){
      int mid = (l+r)/2;
       mergeSort (arr,l,mid);
       mergeSort (arr,mid+1,r);
       
       merge(arr, l , mid ,r);
    }
    }
    ```