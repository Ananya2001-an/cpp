### C++ basics

<hr>


### Diff between C++ and Java

| CPP      | Java         |
| -------- | ------------ |
| Vector   | ArrayList    |


### C++ STL

- `#include <bits/stdc++.h>` includes almost all standard C++ headers. It’s a "super header" file that brings in nearly everything in the C++ Standard Library, including `<iostream>, <vector>, <string>, <algorithm>, <numeric>`, and many others. 

- In C++, `using namespace std;` is a directive that brings all the names from the std namespace into the global namespace, making it easier to use standard library components without having to prefix them with std::.

- Find min and max elements in a list or between 2 no's. For entire container like a vector use minelement and maxelement methods to return iterators. Deref them to get values.
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;

    int main() {
        //1.
        auto result = minmax(10, 20);
        auto result = minmax({10, 20, 5, 15});
        cout << "Minimum: " << result.first << endl;  // Outputs: 10
        cout << "Maximum: " << result.second << endl; // Outputs: 20

        //2.
        int minimum = min(a, b);
        int maximum = max(a, b);
        int minimum = min({10, 20, 5, 15});
        int maximum = max({10, 20, 5, 15});

        //3.
        vector<int> v = {5, 2, 9, 3, 7};
        int min = *min_element(v.begin(), v.end());
        int max = *max_element(v.begin(), v.end());
    }
    ```

- **Vectors** are like smart arrays. They store data just like arrays but unlike fixed sized arrays, vectors can grow or shrink by themselves.

    - `vector<int> v` -> declaration of vector
    - `v.size()` -> size
    - `v.push_back(x)` -> inserts an element x at the back of the vector
    - `v.pop_back()` -> removes the last element from the vector
    - `int ith_element = v[i]` 
    - `v.begin()` -> v.begin() returns an iterator(coming soon) pointing to the first element in the vector v
    - `v.end()` -> v.end() returns an iterator pointing to the position just after the last element in the vector v
    - `v.clear()`
    - ```cpp
        // vector iterator
        vector<int> v = {1, 2, 3, 4};
        for (vector<int>::iterator it = v.begin(); it != v.end(); ++it) {
            // Access the current element using *it
            cout << *it << endl;
        }
        ```
    - In C++, the auto keyword is used for automatic type deduction, it allows the compiler to automatically deduce the type of a variable based on its initializer.
        ```cpp
        vector<int> vec = {1, 2, 3, 4, 5};

        // Using auto with iterator
        for (auto it = vec.begin(); it != vec.end(); ++it) {
        cout << *it << " "; // 1 2 3 4 5
        }
    

        // Using auto with range-based for loop
        for (auto& num : vec) {
            num *= 2; // Modify each element since iterator num is using reference
        }
        ```
    - A reverse iterator is typically declared using the `rbegin()` and `rend()` member functions of a container. These functions return reverse iterators that point to the last element and the first element of the container, respectively.
    
    - `int sum = accumulate(v.begin(), v.end(), 0)` -> It returns the result of accumulating all the values in the given range with specified initial value. The default operation is to add the elements up, but a different operation can be specified:- `accumulate(prefix.begin(), prefix.end(), 1, multiplies<int>());` gives product of all values. 

    - This function assigns a partial sum **(prefix sum)** of the corresponding elements of a vector to every position of the second array.
        ```cpp
        vector<int> prefix_sum(v.size()); // creating a new vector with same size as v
        partial_sum(v.begin(), v.end(), prefix_sum.begin()); 
        ```

    - ```cpp
        vector<int> v = {2, 3, 5, 6, 3};
        replace(v.begin(), v.end(), 3, 8); // now, v = {2, 8, 5, 6, 8} as all old values 3 get replaced with 8
        ```
    
    - ```cpp
        vector<int> v1 = {1, 2, 3};
        vector<int> v2 = {2, 2, 3, 4};
        vector<int> v(v1.size() + v2.size()); // size of merging vector must be equal to v1.size + v2.size()
        merge(v1.begin(), v1.end(), v2.begin(), v2.end(), v.begin());
        ```

    - `is_sorted(v.begin(), v.end())` -> check if vector is sorted.

    - `reverse(a.begin(), a.end());` -> reverse a vector

    - **Sorting**
        ```cpp
        vector<int> vec = {3, 1, 4, 1, 5};
        
        sort(vec.begin(), vec.end());

        //stable_sort() is similar to sort(), but it ensures that the relative order of equal elements remains unchanged after sorting.
        stable_sort(vec.begin(), vec.end()); 

        //partial_sort() partially sorts the range such that the smallest k elements are sorted in ascending order.
        partial_sort(vec.begin(), vec.begin() + 3, vec.end());

        //nth_element() rearranges the elements such that the element at the nth position is in its correct sorted position, and all elements before it are less than or equal to it, while all elements after it are greater than or equal to it.
        nth_element(vec.begin(), vec.begin() + 2, vec.end()); 
        ```

    - **Searching**
        ```cpp
            vector<int> vec = {3, 1, 4, 1, 5};

            //find() is a linear search algorithm that searches for a specific value within a range and returns an iterator to the first occurrence of the value if found, or the end iterator if the value is not found.
            auto it = find(vec.begin(), vec.end(), 4);


            //binary_search() is a binary search algorithm that checks whether a value exists in a sorted range and returns true if the value is found, or false otherwise.
            bool found = binary_search(vec.begin(), vec.end(), 4);


            //lower_bound() returns an iterator pointing to the first element in the range that is not less than (i.e., greater than or equal to) the given value.
            auto it = lower_bound(vec.begin(), vec.end(), 2);  // Finds the first occurrence of value 2 in vec
            cout << *it; // dereferencing the value


            //upper_bound() returns an iterator pointing to the first element in the range that is greater than the given value.
            auto it = upper_bound(vec.begin(), vec.end(), 2);  // Finds the first element greater than 2 in vec
        ```