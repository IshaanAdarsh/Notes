# STL: 
- STL provides a range of containers, such as vectors, lists, and maps, and algorithms for searching, sorting and manipulating data.

## Pair:
- Present in the Utility Library and used to link 2 inputs into a single structure. (They have some relationship)
```cpp
void explainPair() {

// Simple pair
pair<int, int> p = {1, 3};
cout «< p.first << " " < p. second;

// Nested Pair
pair<int, pair<int, int>> p = {1, {3, 4}};
cout << p.first << " " < p.second. second < " " < p. second. first;

// Use pairs as a data type (for arrays in this case)
pair<int, int> arr[] = { {1, 2}, {2, 5}, {5, 1}};
cout << arr[1].second;
}
```

## Vector:
- Vectors are the same as dynamic arrays with the ability to resize itself automatically when an element is inserted or deleted, with their storage being handled automatically by the container.
- `vector<object_type> variable_name;`

```cpp
// Sytnax:
vector<int> v;                                   // Creates a vector storing int data type called v

// Example:

// Pushing values into the vector (emplace better than push)
v.push_back(1);
v.emplace_back(2);

// Can create vector of pairs
vectorspair<int, int>>vec;
v.push_back({1, 2});
v. emplace_back(1, 2);

// Creates a vector of size 5 and all values inside it are 20 -> [20,20,20,20,20]
vector<int> v1(5, 20);

// Copy contents of a vector into another
vector<int> v2(v1);
```

### Functions to implement in Vector:
```cpp
// begin() -> It returns an iterator pointing to the first element of the vector.
vector<int> v1;
auto iterator = itr;
itr = v1.begin();

// end() -> It returns an iterator pointing to the element theoretically after the last element of the vector.
auto iterator = itr;
itr = v1.end();

// push_back() -> It accepts a parameter and insert the element passed in the parameter in the vectors, the element is inserted at the end.
v1.push_back(1);

// insert() -> It is used to insert an element at a specified position.
auto it= v1.begin();
v1.insert(it,5);               //inserting 5 at the beginning

// erase() -> It is used to delete a specific element
vector<int> v1;
auto it= v1.begin();
v1.erase(it);                  // erasing the first element

// pop_back() –> It deletes the last element and returns it to the calling function.
v1.pop_back();

// front() –> It returns a reference to the first element of the vector.
v1.front();

// back() -> It returns a reference to the last element of the vector.
v1.back();

// clear() –> Deletes all the elements from the vector.
v1.clear();

// empty() –> To check if the vector is empty or not.
v1.empty();

// Some Extra functions:
cbegin() – it refers to the first element of the vector.
cend() – it refers to the theoretical element after the last element of the vector.
rbegin() – it points to the last element of the vector.
rend() – it points to the theoretical element before the first element of the vector.
crbegin() – it refers to the last element of the vector.
crend() – it refers to the theoretical element before the first element of the vector.
max_size() – returns the maximum size the vector can hold.
capacity() – it returns the current capacity of the vector.
```

#### Loop through a vector:
```cpp
for (vector<int>::iterator it = v.begin(); it != v.end(); it++){
  cout << *(it) << " ";
}

// OR

for (auto it = v.begin(); it != v.end(); it++) {
cout << *(it) << " ";
}
```

## List:
- A list in [STL](https://takeuforward.org/c/c-stl-tutorial-most-frequent-used-stl-containers/ "STL") is a contiguous container that allows the inserting and erasing of elements in constant time and iterating in both directions.

```cpp
// Syntax
list<object_type> variable_name;
```

### Functions in List:

```cpp
// push_back(): To insert an element at the end of the list.
list<int> li;
li.push_back(110);
li.push_back(220);

// push_front(): To insert an element at the front of the list.
list<int> li;
li.push_front(110);
li.push_front(220);

// pop_back(): Deletes the last element of the list.
li.pop_back();

// pop_front(): Deletes the front element of the list.
li.pop_front();

// front(): It gives a reference to the first element of the list.
li.front();

// back(): It gives a reference to the last element of the list.
li.back();

// reverse(): Reverse the list.
li.reverse();

// sort(): Sorts the list in ascending order.
li.sort();

// size(): Returns the number of elements on the list.
li.size();

// empty(): To check if the list is empty or not.
li.empty();
```
