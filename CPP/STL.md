# STL

for all libraries : #include< bits/stdc++.h>

S. No. | STL Container Name | Internal Data-Structure | Time Complexity

1. Unordered Set : Hash Table
   (A hash table uses a hash function to compute an index)
   For Insert, Search, Delete:
   Best: O(1)
   Avg: O(1)
   Worst: O(N)

2. Set : Red Black Tree
   (self-balancing binary search tree – maintains the height of tree log N)
   For Insert, Search, Delete:
   Best: O(log N)
   Avg: O(log N)
   Worst: O(log N)

3. Unordered Map : Hash Table
   (A hash table uses a hash function to compute an index)
   For Insert, Search, Delete:
   Best: O(1)
   Avg: O(1)
   Worst: O(N)

4. Map : Red Black Tree
   (self-balancing binary search tree – maintains the height of tree log N)
   For Insert, Search, Delete:
   Best: O(log N)
   Avg: O(log N)
   Worst: O(log N)

5. Priority_queue : Max Heap
   Insert/Push: O(log N)
   Delete/Pop: O(log N)
   Peek/Top: O(1)

6. Stack : Linked List
   Push: O(1)
   Pop: O(1)
   Top: O(1)

7. Queue : Linked List
   Push: O(1)
   Pop: O(1)
   Front: O(1)
   Back: O(1)

## Pairs :

```cpp
=) pair<int, int> p = {1,3}; // the curly braces are like kinda good.
=) pair<string, int> p("preetam", 12);
=) p.first;
=) p.second;
```

a pair has two parts, first and second.

## Vectors :

```cpp
vector<int> v(size);
v.push_back(1);
v.emplace_back(2); // NOTE : this takes inn only the to be passed constructor arugments.
```

=) vector< type> v(size, default_value);

NOTE: itreators are pointers that point to certain elements in the container.

=) vector< int>::iterator it = v.begin(); // a pointer to stargting element of the vector. or =) auto it = v.begin();
=) v.end() : gives a pointer to memory after the last elemtn and hence its best to just use : v.end()-1 to access the element at the last.
=) v.rbegin() : assumes that the vector is reverse and hence will return the last element
=) v.rend(): will give us the memory before the first element and we can add 1 to access the first element.(kinda sus -\_-)

IMPORTANT NOTE :even the ++ operations and other pointer operations will be reversed and be like asif the list is reversed.

NOTE: a small snippet to iterate through a vector is :

```cpp
for(auto it = v.begin(); it != v.end(); v++){
    cout << *(it) << " ";
}
// or
for(auto it : v){
    cout << it;
}

```

=) v.erase(starting_pointer) : removes one element
=) v.erase(start_pointer, end_pointer) : removes elements between (end is not inclusive)

=) v.insert(pointer, value);
=) v.insert(pointer, number_of_repeats, value) : to add element multiple times.

IMPORTANT : =) v.insert(starting_position, Starting_address, Ending_address) : this is for inserting from another vector or memory onto a position in current vector. This is useful and can be used to insert part of one vector into another vector.

// NOTE : in erase and insert function, the end pointer is non inclusive.

=) v.pop_back() : remove last element.

=) v.swap(other_vector) : will swap the vectors.
=) v.clear() erases the entier vector.

<hr>

## List

List are same to vector but we can perform operations on both ends of the ds.
QUESTION : why use list ?
ANSWER : insertion is faster since it maintains a linked list. However accesss is faster in vector.

```cpp
list<int> ls;
```

=) ls.push_back();
=) ls.emplace_back();

=) ls.emplace_front();

## dequeue : double ended list :

dequeus has all function like vector and list : its just a double ended queue.

<hr>

## Stack :

```cpp
stack<int> st;
```

=) st.push(value);
=) st.emplace(value);
=) st.top();
=) st.pop();
=) st.empty();
=) st.swap(st2);
=) st.size();

<hr>

## Queue

=) queue< type> name ;
=) q.push(value);
=) q.emplace(value);
=) q.pop();
=) q.back() : returns value at the back(unlike q.end() that will return pointer)
=) q.front() : return value at the front

<hr>

## priority queue :

keeps the element with most priority at top :

=) priority_queue< type> pq;
=) pq.push(value)
=) pq.emplace(value);

=) pq.pop();

NOTE : for making a min heap we use :

```cpp
priority_queue<int, vector<int>, greater<int>> pq;
```

IMPORTANT QUESTION : how do we define priority in custom types for sorting and stuff ??
ANSWER : We can actually defind the priority using two methods :

1. using class :

```cpp
class Person{
    public :
        int age, height;
    // we are doing operator overloading through this
    // NOTE if p2 has more priority, this should return true.
    bool operator<(const Person& p1, const Person& p2){
        return p1.age < p2.age;
    }
}
```

we simply override the less than operator and that is it.

2. using struct :

```cpp
struct Person{
    public :
        int age, height;
}
// this is an structure which implements the
// operator overloading
struct CompareAge {
    bool operator()(Person const& p1, Person const& p2)
    {
        // return "true" if "p1" is ordered
        // before "p2", for example:
        return p1.age < p2.age;
    }
};
void main(){
     priority_queue<Person, vector<Person>, CompareAge> Q; // this will use Compare height as the struct containing the override.
}
```

the way this helps is that in STL DS that use priority like priority queue, we can pass this inn as a template argument.

<hr>

## Set

stores SORTED and UNIQUE :

=) set< type> name;
=) st.insert(1);
=) st.emplace(1);

begin(), end(), rbegin() etc work the same way.

=) st.find(3) : returns pointer that points to this address, has type iterator.

IMPORTANT NOTE : upon not finding any element using st.find(), the operation returns =)st.end(); which is a pointer to the end of the st.

=) st.erase(value) : removes element in logarithmic time.
or
=) st.erase(iterator) : removes the value at iterator at constant time.

=) st.erase(start_iterator, end_iterator) : to remove a range of elements.

NOTE: the erase function is overloaded and passing the iterator is faster than passing the value to be removed. which make sense.

=) st.count(value) : will check the count of element which will be either 0 or 1 for set since so duplicates are stored.

IMPORTANT :

=) st.lower_bound(value) : The lower_bound() method in C++ is used to return an iterator pointing to the first element that is equal to value if it is present OR it will point to the immediate greater value.
NOTE: this uses binary search internally and hence must be used on sorted data.
=) st.lower_bound(start, end, value) : this overload helps perform the binary search operation within the given range.

```cpp

set<int> set = {1,2,3,4,8,12,19};
set.lower_bound(set.begin(), set.end(), 8); // this will be 8
set.lower_bound(set.begin(), set.end(), 9); // since there is no 9, this will return 12
set.lower_bound(set.kkbegin(), set.end(), 30); // since the element is out of range, this will return set.end();

```

=) st.upper_bound(value) : It returns an iterator pointing to the next greater element.
=) st.upper_bound(start, end, value) :

```cpp

set<int> set = {1,2,3,4,8,12,19};
set.upper_bound(set.begin(), set.end(), 8); // this will be 12
set.upper_bound(set.begin(), set.end(), 9); // since there is no 9, this will return 12
set.upper_bound(set.begin(), set.end(), 30); // since the element is out of range, this will return set.end();

```

NOTE: lower bound and upper bound in conjunction are helpful for setting up pointers at start and end of a range.

<hr>

## Multiset

keeps multiple occurences of elements in sorted manner.

=) multiset< type> ms;
=) ms.insert(value);
=) ms.emplace(value);

=) ms.erase(element) : removes all occurences of the element
=) ms.erease(iterator_to_element) : removes a single instance from the set.

=) ms.find(element) : returns pointer to the first occurence of the element in the multiset.

=) ms.count(value) : returns the number of occurences of that value in the ms.

<hr>

## unordered set :

same as set but stores Unique and non sorted.
IMPORTANT NOTE : unordered_set is faster in operations that the other 2 counterparts since it does not maintain sorted order and hence operations take O(1). Uses internally hashmap.

all other function are the same.

<hr>

## map :

map stores in SORTED ORDER OF KEY and Keys are unique.

=) map< type, type> mpp;
=) map[ key] = value
=) map.insert({key, value});
=) map.emplace({key, value});

NOTE: maps internally store pairs and that makes map.emplace({key, value}) possible.

=) map.begin()
=) map.end()

=) map.find(key) : returns iterator to that key

since data is sorted, we can use map.lower_bound(); and map.upper_bound() based on the key.

<hr>

## multimap :

multimap is Sorted HOWEVER Keys can repeat

the only different is :

=) mm.find(key) : will return the first instance of that key in the mm.

<hr>

## Algorithms :

=) sort(begin, end) : sorts data where end is non inclusive.

=) sort(begin, end, comparator) :

IMPORTANT : comparators are very essential as they define how two elements are compared eg. we can use greater< int> for sorting in decreasing order.

-> Comparators are noting but boolean returning function pointer.

```cpp
// comparator for sorting pair based on the second and then after the first
bool comp(pair<int, int> p1, pair<int, int> p2){
    if(p1.second < p2.second) return true;
    else if(p1.second > p2.second) return false;
    else{
        if(p1.first > p2.first) return true;
        else return false;
    }
}
```

=) binary_search(start, end, value_to_search) : returns true and false based on stuff.

=) next_permutation(start, end); this helps go over all the permutations of a string and we can cimply call next_permutation and it will make changes to the string and enable us to access all permutations like this :

```cpp

string s = "123";

while(next_permutation(s.begin(), s.end())){
    std::cout << s << std::endl;
}

```
