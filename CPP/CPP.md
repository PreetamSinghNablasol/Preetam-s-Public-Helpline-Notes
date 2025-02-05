# C Plus Plus

-> Preprocessor files : start with #

-> Main function does not need to retun 0 as it does by default return 0.

-> Preprocessor commands : #include, #define, #prag etc.

-> inlcude inclues the library code

-> define replaces every word into the other word eg #define Integer int.

-> compiling to .class files > then linking is done.

-> Here are various g++ commands :

> g++ -o main.exe hello.cpp : to specify the output name also.
> ./a.exe : to run the compiled code
> g++ -S hello.cpp : to only compile the file and not assemble it or link it this will make file_name.s
> g++ -c hello.cpp : to compile and assemble the file and not link it

-> NOTE: .h file contains only the function prototyping :) if we make one for including of various libraries.

QUESTION : How to compile and link various files ?
ANSWER : suppose we have various files : hello.cpp and helloworld.cpp

> g++ -c helloWorld.cpp hello.cpp : to make the object files of the 2 cpp files.
> g++ -o main.exe helloWorld.o hello.o : to link th etwo files .

-> we can use static to fix linking errors in case of ambiquity issues. Since the code will then become only accessible inside of the Translation unit.
This is called internal linking.

-> we can make a function inline also to fix somewhat ambiguity issue as it will just simply replace a line of code with the linline returned value.
Hence the linker will simply just replace every line where the function is mentioned and replace it with the inner content of hte return value of the function.

-> sizeof() or sizeof

-> Header file : Header files are better used to include prototypes of the already existing functions and this makes it eazy for us.

-> pragma is an instruction of preprocesor and : pragma once is a header guard that will no tallow same header mentioned in a single file twice.

-> but a better header guard is :

```cpp

#ifndef _def
#define _def
```

but pragma once is new :)

-> includes with <> are inside include path folders whereas in string "" we mention files that are in relative to current file.
we can even use "" for iostreams and other default files :).

QUESTION : why does iostream not have a .h extention?
ANSWER : to differentiate between c and cpp library.

-> void pointer type does not care the type of data that the pointer will hold. However we cannot change value of a value in void pointer address since we dont know the type.
-> nullptr : for making a null pointer.

-> char\* buffer = new char[8]; will make a buffer to allocate memory but we can free up memory using delete[] buffer.

-> =) memset(pointer, value , size) : will fill the next memory upto size with the value starting from the pointer.

-> classes make variables are private by default.

QUESTION : what are the difference between struct and class?
ANSWER : There is no major difference except : A class is private by default whereas a struct has stuff as public.
We literally need to switch the class keyword with struct and that is the difference.

-> Inheritance is possible in sturcuts BUT not recomended.

IMPORTANT -> Static has 2 different meanings depending on inside a class or inside a translation unit. We know about class but, static in scope of a Translation unit, the linker will not link that function to any outside file as the function will then be only available in the translation unit it is defined inside of.

-> =) extern : making a variable extern means that the definition of that variable is somewhere outside in another translation and unit and must be looked up in another translation unit. The linker will hence look for the definition in global scope.

-> we access the internal static variables asif the class is a namespace eg :

```cpp
struct Entity{
    static int x, y;
    static void print(){
        std::cout<< x << " "<< y << std::endl;
    }
};
int Entity::x;
int Entity::y;
```

NOTE: we cannot access these static variabes directly using objct names without prototype mentioning them in the global scope.(it throws unknown external symbol.)

-> It makes sense why the static variables inside classes are treated like namespaces, since classes are then only just giving the static variabels a scope and nothing else.

-> Enum, a way of giving text values to integers. Enumeration. So its just a way to name values.
-> Enums can have types of int or char only since we need them to be integer.

```cpp
#include <iostream> // pre processor statements

enum Example : char
{ // by default value is 0, 1, 2 and 3
    A, B, C
};

int main(){ // entry point
    Example value = B;
}
```

-> Enums inside of classes are kinda like static and hence are accesss using Class::EnumName.Enum convention.

```cpp

class Preetam{
    enum num : int{
        A, B, C
    };
};

int main(){
    std::cout<< Preetam::num.A << std:: endl;
}
```

-> we can delete default constructor using Class() = delete; and this will basically delete the default constructor making is not available to be used. This can come in handy incase we want only some static sectio nof code accessible.

-> Destuctor will run when an object is cleaned up. (Be it being deleted using delete or when scope ends.)

-> we can call the descturctor manually like :) obj.~Demo()

-> Inheritance is done using : and we need to specify the access specifier too.

```cpp
class Player : public Entity
```

-> Virtual Functions : virtual function are functions can be modified in the child class.

-> V table keeps a maping so that what version of virtual function was called can be marked up.

-> Making a function virtual will mean that we mark the function for the virtual table and then incase of child class overriding the function, we want to check the V table if the reference type was of child or parent type and depending on them calling the function depends.

-> we can use override

```cpp
int getInt() override { return num;}
```

NOTE: there is additional cost associated with v functions. 1> keeping entry in the table 2> checking the table incase of function invocation.

-> Pure virtual functions are used in interfaces and we need to instanciate them in child class compulsorily.

-> cpp does not have interface keyword and hence a function with virtual functions will be an interface.
NOTE: we need to compulsorily define the virtual functions defined in the parent class into the child class.

-> private, public and protected are the only visibility modifier.

-> private means only the class can access the variables. (Except for friend LMAO).

-> protected means the class and subclasses can access.

-> public means anyone can access.

IMPORTANT OBSERVATION : we can access value of a pointer using : *pointer and also change value of a pointer with dereferencing only like *ptr = 12 Hence dereferencing not only exposes the internal value for reading but we change the value by dereferencing.

-> we can allocate arrays in heap also using new keyword :

```cpp
int* another = new int[5];
delete[] another;
```

-> things allocated using new will stay till its deleted.

-> cpp 11 has a std:: array that is very useful and can be used but we dont do this since

NOTE: sizeof operator for stack allocated array will return the actual size of whole array in the memory, however a heap allocated one will give the size of the pointer variable and this is an important observation.

IMPORTANT NOTE: incase we are trying to give size of array like :

```cpp
const int x = 12;
int ex[x];
```

this will throw error since cpp wants us to give size at compilation time and hence we need to make 'x' static in order to allocated an array of the given size.

```cpp
#include <array>
std::array< int, size> array;
std::cout << array.size() << std::endl;
```

-> string = const character array.

```cpp
const char* str = "Preetam";
```

-> we need to make character string a const because strings are immutable.
-> strings end with null and that is how we know how string ends.

```cpp
#include <string>

const char* str1 = "preetam"; // automatically gets null "/0" at end
const char[5] str2 = {'P', 'r', 'e', 'e', 't'}; // will not end with "/0"

// std:: string
const std::string string = "preetam";
```

=)strlen(s) : string length
=) strcpy(s) : string copy
=) s.size() : when using std::string

-> for adding two strings :

```cpp
std::string name = "hello";
name += " there";

or

std::string preetam = std::string("hello") + " hello";

or

std::string preetam =  "preetam"s+ "hello";
// here s is an operator that returns std::string
```

we do this becase incase of std::string the + opeartor is overloaded :) hence we need one of the string to be of type std::string.

-> to find a substring we use =)name.find(substring) and incase the string was not present it returns std::string::npos.
we can use this to check contains since there is no other contains function.

-> since string ends with "/0" its just has sizes 1 bigger than the actual size.

IMPORTANT NOTE : CPP has pure pass by reference i.e.
-> passing values without a pointer actually passes in a copy of the value even in the case of an object being passed. eg ;

```cpp
void print(std::string string){
    std::cout << string << std::cin;
}
```

in this code unlike java, if we pass a string it will not be taken in as a reference but as a copy. hence we shoul make it a const reference.

```cpp
void print(const std::string& string){
    std::cout << string << std::cin;
}
```

-> String literal is a series of characters between " " that are non dynamically allocated.
-> String literals are stored in read only memory and hence its not defined in cpp how making changes to individual characters in string should work.

```cpp

char* str = "preetam";
str[2] = 'a'; // this behavior is undefined.
```

-> hence in order to actually edit individual characters make it in array format like :

```cpp
char[] str ="Preetam";
str[2] = 'b';
```

-> Other characters : note the type sof prefex attatched.

```cpp
const char* name = u8"preetam";
const wchar_t* name = L"preetam"; // 2 bytes on window and 4 on linux
const char16_t name = u"preetam";
const char32_t name = U"preetam";
```

-> there also exist std::wstring (L"preetam") and std::u32string (U"preetam") and std::u16string (u"preetam")

-> we can make a multiline string by using R

```cpp

cons tchar* prt = R"(preetam
is the
king)";
```

the paranthesis are compulsory here and R will then ignore the escape sequence.(beter than using \n)
R stands for raw.

-> const in cpp is more like just a promise that we wont change it. And we can change it actually with help of a few tricks.

-> think about difference between const int* ptr(or int const* ptr) and int\* const ptr are different.(note depends on the side of \* const is written on)

-> a const with method ??

```cpp
int getX() const{}
```

this makes a method incapable of changing the data variabels of the class.

-> NOTE: to make many pointer in same like, the syntax is : int* ptr1, *ptr2, ptr3;

QUESTION : why do we need to make a function const ?
ANSWER :

```cpp
class Entity{
    int m_X, m_Y;
public:
    int GetX() const{
        return m_X;
    }
    void SetX(int x){
        m_X = x;
    }
};

void PrintEntity(const Entity& e){
    std::cout << e.GetX() << std::endl;
}
```

in the above code following are a observations :
-> if GetX() is not const function, we cannot call e.GetX() inside of PrintEntity.
-> The reason for this is that e is a constant reference meaning that we can change what it points to , but we cannot change what value is stored at what it points to.
-> IMPORTANT : hence we can only call those function from entity that promise that they will not change the entity data. This is because entity e is a const reference and threrefore we can only call const functions.
-> this is why sometimes some functions have 2 versions, one with const and one without. Hence makr all functions that do not modify the actual object as const.
-> mutable variables can be changed inside of const functions :) simple.

NOTE: -> suppose if we have a const reference, we cannot assign it to a non const reference. This makes sense since then anyone can assign a const reference to a non const reference and change it -\_-

-> mutable has another functionality with lambdas, that we will see later.

-> Constructor member initialisation list : it is the other way of initialising variables and can be done like this :

```cpp

class Entity{
    private:
        std::string m_Name;
        int m_Score;
    public:
        Entity()
            : n_Name("Unknown"), m_Score(0){
                // constructor code
            }
}
```

IMPORTANT NOTE : always declare member initialiser list in the order we define elements in class as whatever order we write it in the list, they get initialised in the order specified in the class. Some compilers can throw errors incase we dont specify the list in the correct order.

**OPTIMIZATION : **
IMPORTANT QUESTION : why use member initializer list?
ANSWER : There is an actual functional difference, normally when we use constructor function to initialize a variable, it gets initialised twice !!!! YES TWICE. Once it gets initialised in the class body and another in the constructor. HOWEVER, member initializer list makes sure that the variable only gets initialized once :)

```cpp
class Entity{
    private :
        std::string preetam; // first initialization
    public :
        Entity(){
            preetam = "preetam"; // second initialization.
        }
}
```

-> Stack objects are declared for the scope they are in.(since they are in stack)

-> Heap memory stays till we flush it using delete.

OPTIMIZATION :
NOTE: if possible, always create objects on stack.

QUESTION : what are the cases where we need Stack Allocation?
ANSWER : look at the code snipped below :

```cpp
std::string* e;
{// scope
    std::string st = "preetam"
    e = &st;
}
// here e points to the st but st value is destroyed since scope ended
```

in the above code, note that e will point to st however, scope of st has already ended hence value is cleaned. Meaning e points to a garbage location.

Hence we make use of stack allocation in suck cases where we want memory to live longer than scope.

NOTE: new keyword returns a pointer to heap memory and hence we always use pointer to store the value returned new keyword allocation.

```cpp
std::string* e;
{
    std::string* st = new std::string("Preetam");
    e = st;
}
```

-> Free List : keeps track of free memory and new keyword looks for memory here :)

-> we can use =)new() to specify the location at which we want to allocate the memory

```cpp
Entity* ptr = new Entity();
Entity * newPtr = new(ptr) Entity();
```

-> Implicit means automatic.

IMPORTANT : -> TYPE CONVERSION :

```cpp
class Entity{
    private:
        std::string m_Name;
        int m_Age;
    public:
        Entity(const std::string& name): m_Name(name), m_Age(-1){}
        Entity(int age): m_Name("Unknown"), m_Age(age){}
        std::string getName(){
            return this.m_Name;
        }
};
void printEntity(const Entity& entity){
    std::cout << entity.getName() << std::endl;
}

int main(){
    Entity a = (std::string)"Cherno"; // since there exists a suitable constructor hence this is possible.
    Entity b = 22;
    printEntity(22);
    std::cin.get();
}
```

how we are able to call printEntity function with 22. This is because 22 will get converted implicitly into Entity since a constructor exists that takes inn a number.

NOTE: implicit conversion only occurs upto one time, meaning implicit convertion wont occur if the convertion needs to happen twice.

-> explicit can be put in front of a constructor and that will not allow for such implicity converstion.

-> operators are like functions and we can overload them like :

```cpp
// inside classs
class Vecortor{
    Vector operator+(const Vector& other) const{
        return Vector(x+other.x, y+ other.y);
    }
    Vector add(const Vector& other) const{
        return operator+(other); // we can use operator+() like a function too :)
    }
}
// outside class

bool operator== (const Vector& v1, const Vector& v2){
    return (v1.m_x == v2.m_x) && (v1.m_y == v2.m_y);
}

```

IMPORTANT QUESTION : How does overloading of << work ?
ANSWER : the oveloading to print output to console incase of our own datatypes is :

```cpp
std::ostream& operator<<(std::ostream& stream, const Vector& other){
    stream << other.x << ", " << other.y; // we are adding to the stream
    return stream;// we are returnign the stream.
}
// In the above code, basically we are taking inn a stream and a Vector, we are writing to the stream and returning it, then the stream is visible on the console.
```

IMPORTANT OBSERVATION : Note how in the above two example, one is defined inside of the class itself and other is defined outside of class and hence we need to pass inn both the operands.

-> this is not a reference but a pointer to current class and hence we need -> operator.

NOTE: this is actually a pointer that is const, ie the actual pointer is const and not the value. AND IMPORTANT OBSERVATION is that inside of a const function, this is a const pointer !! meaning

```c++
Entity* const e = this; // this keyword inside normal methods
const Entity* const e = this; // this keyword inside const function
```

-> There is a case where we can delete an object from within using delete this inside a member function.

-> with the help of constructors and destructors we can create a scoped pointer.

```cpp
class Entity{
    std::string m_Name;
    Entity(std::string name): m_Name(name){}
};
class EntitySmart{
    private:
        Entity* m_Ptr;
    public:
        EntitySmart(Entity* ptr); m_Ptr(ptr){}
        ~EntitySmart(){ delete m_Ptr};
}
int main{
    {
        EntitySmart e = EntitySmart(new Entity("Preetam"));
    }
}
```

The above code is example of our own smart pointers.

-> Smart Pointers : A smart pointer is used to automate the delete process :)

-> Unique Pointer : scoped pointer :). NOTE : the reason its called unique pointer is because it is unique and we dont create a copy since after the scope ends, the pointer will point to garbage.(this is done by deleting the copy constructor lol)

-> #incldue <memory>

```cpp
{
    std::unique_ptr<Entity> entity = std::unique_ptr();
    or
    std::unique_ptr<Entity> entity = std::make_unique(new Entity());
    or
    std::unique_ptr<Entity> entity(new Entity());
}
```

IMPORTANT NOTE: we are making the entity pointer itself stack allocated. Also we are calling constructor of make_unique because of exception safety.

NOTE : the constructor for this pointer is explicit hence no shortcuts :(

-> we access the elements then using arrow opeartor

-> Shared Pointer : uses reference counting i.e keeping track of how many reference to the pointer exist and if that reaches 0, the shared pointer frees memeory.

-> Shared pointers allow us to pass inn the pointer and create copy. HENCE, the memory is cleaned only when every pointer pointing to the heap memory goes out of scope.

```cpp
std::shared_ptr<Entity> sharedEntity = std::make_shared<Entity>();
std::shared_ptr<Entity> sharedEntity2 = sharedEntity;
```

-> Weak Pointer : we can copy the shared pointer into a weak pointer and that will not change the reference count

```cpp
std::shared_ptr<Entity> sharedEntity = std::shared_ptr<Entity>(new Entity()); // DONT USE THIS WRONG
or
std::shared_ptr<Entity> sharedEntity = std::make_shared<Entity>();
std::weak_ptr<Entity> weak = sharedEntity;
```

OPTIMIZATION:
Shared pointers and smart pointer have some overhead and when possible avoid using them.

IMPORTANT NOTE : so in case of unique pointer we used make_shared because of exception handling, BUT in case of shared pointer, we are using make_shared because then we dont have to call the new keyword. This is because we want to keep track of reference count and calling the Entity with new is like an extra reference count !!! Hence all that stuff :)

NOTE: eazy way to assigne values to a struct is :

```cpp
struct Vector{
    float x, y;
};
int main(){
    Vector a ={ 2, 3}; // shorthand
}
```

-> IMPORTANT OBSERVATION : unlike in java where if we make a copy of an object we actually make a new reference, in CPP we actually create a new fresh object with copy of internal values of the original object. Hence to create a copy by reference we need to actually make a copy of the reference.

=) memcpy(destination, source, size) : for making a copy from the memory into a new address.

QUESTION : when do we need to make changes to the copy constructor ?
ANSWER : WE have to remember that by default the copy constructor does a shallow copy, and hence its very essential that we actually modify the copy constructor incase there are pointers as member variabels and hence shallow copy can be devastating. Hence incase of making custom classes with pointer and reference as member variables, make sure to change the copy constructor.

```cpp
class String{
    String(const String){
        // logic to copy data.
    }
}
```

-> By default the copy constructor just performs a memcpy() and hence the copy is a shallow copy.

-> we can evey remove the copy functionality using this :

```cpp
class String{
    String(const String) = delete;
}
```

OPTIMIZATION :
NOTE: always make sure to pass in any objects and stuff as reference.

IMPORTANT NOTE: -> Note that when we override the constructor, the return value of the overload is not what it seems

```cpp
class String{
    public :
        char* str;
        String(const char* ptr){
            strcpy(this->str, ptr);
        }
        char& operator[](int index){
            return str[index];
        }
};
int main(){
    const char* ptr = "Preetam\0";
    String s = String(ptr);
    s[1] = 'h';
    std::cout << s[1] << std::endl;
    std::cin.get();
}
```

in this case, we cant just access usign the overload but, even make changes :)

-> we can overload the arrow operator also and this can come in handy in some cases :)

NOTE: arrow operator can be used to find the offset of data members in memory. i.e offset is like if the data started from 0, then at what position will each member be.

```cpp
struct Vector{
    float x, y, z;
};
int main(){
    int offsetX = (int)&((Vector*)nullptr)->x; // we can use 0 inplace of nullptr too
    int offsetY = (int)&((Vector*)nullptr)->y;
    int offsetZ = (int)&((Vector*)nullptr)->z;
}
```

int above code, the offsets will be 0, 1 and 2 respectively. :) wont use this, but can come in handy.

<hr>

## JUICY PARTS

<hr>
<hr>

#### std::vector :

std::vector is a dynamic array. ITS CALLED VECTOR IS KINDA MISTAKE. ITS MORE LIKE AN ARRAYLIST !!

OPTIMIZATION :
QUESTION : should we make vector to pointer (std::vector(Vertex\*)) or vector to normal type (std::vector(Vertex)) ?
ANSWER : it depends, becasue stack is always what we should aim for if possible for optimization. But sometimes we might need to assign a vertext to pointers.

=) vec.pushBack(element) : we can pass inn elements.
=) vec.size() : for getting size

-> indexing is possible in vectors.

-> for each loop format :

```cpp
for( Vertex& v : vertex){ // make sure to use reference here

}
```

=) vec.erase(memory_address) : to erase element at given address. One good way is :

```cpp
int main(){
    std::vector<Vertex> vertices;
    vertices.erase(vertices.begin() + 2); // to remove the second element.
}
```

=) vec.clear() : to erase everythhing

#### IMPORTANT OPTIMIZATION IN VECTORS :

-> One very imoprtant thing to know while optimizing is, WHEN IS COPYING HAPPENING !!!
-> to Test that we can add copy constructor and check how many times its called.

Check the code below :

```cpp
int main(){
    std::vector<int> arr;
    arr.push_back(1);
    arr.push_back(2);
    arr.push_back(3);
};
```

The above code causes 6 copies !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! Here is how
-> for each element copying it from main to the actual memory of the vector itself (3 copies)
-> resizing of the vector from 1 to 2 and then 2 to 3 will again copy all 3 elements :)

But the optimizations are very easy.
-> first to deal with the size doubling of the vector, if we know the number of elements there will be in our vector we can simply reserve memory like :

```cpp
std::vector<Vertex> vertices;
vertices.reserve(3);
```

QUESTION : what is difference between reserve and just passing size in constructor of the vector(or resize)?
ANSWER : passing in size in constructor will not allocate memory to store objects but construct those elements. that is not ideal. reserve will actually reserve the memory for those to come elements and is much more ideal in an envirnoment where we know the size of vector that we want.

this will drop copy from 6 to 3

-> Now we need to resolve the fact that the objects we construct here in main will be copied into the vector and we want to construct them in the actual vector.

=) vec.emplace_back(parameter list) : emplace back just takes inn the parameter list for the elements and then initialize them in the vector itself!!!

```cpp
std::vector<Vector> vertices;
vertices.reserve(3);
vertices.emplace_back(1,2,3);
```

This drops the copies from 3 to 0 !!!!!!!!!!!!

<hr>

#### Static in local scope :

-> If we use static inside of a local scope like inside of a function, the variable will persist till the end of program and will be accesible inside of the function only.
-> the first time the scope is called, the static will be initialised and then will change based on how many times the function is called and what logic the function performs on the variable.

#### Libraries

-> static linking is faster than dynamic linking
-> the include libarary consists of header files that contain the prototyping of the required stuff.

To link in static way :
-> first we include the header file that contains all the functions that contains the list of available functions in the binary.
-> including does not mean adding the static libraries, its just a promise to the compiler that these files are there other files and to make the static lib file available,

NOTE: -> rememember that including and adding binary is different

In CPP we can actually specify the header file while compilation, and then later we can specify the library files while linking.

-> in ide like VS, we can actually specify the libraries in the project compiler itself. and that comes in handy.
( too lazy to check the code and format tho lol)

-> Dynamic linking happens at runtime : the dll files will run along with the program :)
after that we can pull any contents of the library.
-> we do need header file for dynamic library aswell.

there are 3 files in case of dll : XYZdll.lib, XYZ.h, XYZ.dll
Here is how we do it :
-> there is a dll.lib file included with .dll file
-> we compile with header fiel
-> we assemble with the dll.lib file
-> we paste the .dll file in the same directory as the .exe directory

NOTE: THE DYNAMICALLY LINKED LIBRARY NEEDS TO BE IN THE SAME DIRECTORY AS OUR EXE FILE IN ORDER TO WORK.

#### Returning multiple values

-> best way to return two data member from a same function is to make a struct that has those two types variables and use that

-> there are othe ways to return multiple values but the best one is this create a structure way.

-> one way is to make pointer to multple return types in the scope where the function was called and pass them in the function. When we have to value to be returned, just modify the value of the pointer provided.

<hr>

### Templates in cpp :

Templates are infinitely more powerful than generics.

Template is compiler writing code for us.

```cpp
template<typename T> // template parameter and template name. we can use class inplace of typename aswell
void Print(T value){
    std::cout << value << std::endl;
}
int main(){
    Print<int>(5);
}
```

QUESTION : how does this work?
ANSWER : template based code is not in memory untill we call it. And based on how we call it, it gets initialised into memory.

-> its not compulsory to specify angular bracket types when using template class or function.

IMPORTANT : its important to note that templates are used by compilers to write code at runtime and hence we can avoid compiletime issues :

```cpp
template<int N>
class Array{
    private:
        int m_Array[N]; // normally this N needs to be known during compiletime
    public:
        int GetSizes() const {return N;}
};

int main(){
    Array<5> array;
    std::cin.get();
}
```

in the above program, N needs to be known during compiletime but, since template will only enter the memory when we call the template, a verson of array will be created with size 5 :)

-> this is very powerful and fully utilised by STL.

#### Where and where not to use templates.

DONT OVERUSE TEMPLATES !!! because they might become complex.

<hr>

### Stack vs Heap :

-> We allocate memory in stack, the memory is put in memory and stack pointer just, moves. This is why stack allocation is so fast.

-> We allocate memory in heap, the new keyword will check free table that contains information of free block of memory in available in heap.
its calling malloc(). There are lots of steps involved in calling malloc :)

<hr>

### Macros in cpp :

When a program runs, first the preprocessor directives are evaluated and afterwards other things happens.

-> this preprocessor stage is like text editing stage and will decide which code will be passed onn to the compiler.

NOTE: use of define is more than just what seems. we can pass argumanest.

```cpp
#define LOG(x) std::cout << x << std::endl;
int main(){
    LOG("preetam");
}
```

this can come in very handy.

-> we can even use macros to run our program on different configurations for debug mode and production mode.

```cpp
#ifdef PR_DEBUG
#define LOG(x) std::cout << x << std::endl
#else
#define LOG(X)
#endif
```

this small snippet will actually make is so that only if PR_DEBUG is defined the loging will occure in the program.
Some ide like VS allow us to add custom macros for debug mode or other mode.

ALTHOUGH, the better macro for this is :

```cpp
#define PR_DEBUG 0

#if PR_DEBUG == 1
#define LOG(x) std::cout << x << std::endl
#else
#define LOG(X)
#endif
```

hence in the above code, we can just swap PR_DEBUG from 1 and 0 to enable and disable logging.

NOTE: we can enable disable entire code with macros conditional compilation.

-> we can add multipline macros using back slash \ :

```cpp
#define MAIN int main()\
{\
    std::cin.get();\
}
// NOTE : there should be no space after \ :)
```

<hr>

### auto keyword

auto is used to automatically deduce the type of data. There are a few good and bad stuff about this.
This kinda makes cpp a loosely typed language :(

-> The better convention of using auto is to use it when we dont know what type of data some piece of code will return.

NOTE : keep in mind to use auto& incase we need to make a reference and not copy.

we can even use auto as return type :

```cpp
auto function1(){}
```

<hr>

-> constant expression : (constexpr) are those values whose values are fixed and determined during compiletime and are non dependant on others. We can mark constant expressions as constexpr incase.

#### Static arrays : (std::array)

we include < array>

=) std::array< type, size> arr

standard arrays are optimal and we should use them. They warn us if we go out of bounds and have size() and other methods.

<hr>

### Function pointers :

we can make pointers to functions :)

```cpp

void HelloWorld(){
    std::cout << "Hello World!!";
}
int main(){
    auto function = HelloWorld;
    function();
}
```

QUESTION : we used auto but what is the type of a function ?
ANSWER : it is a strange looking syntax :
=) void(\*function_name)(parameters) = function;

```cpp
void printIt(int a){
    std::cout << a;
}
int main(){
    void(*print)(int) = printIt;
    print(12);
}
```

NOTE: majorly just use auto -\_-

-> we can use std::function to define function also :

```cpp
#include<functional>
std::function<void(int, char)> func = intChar;// intChar is stored in func
```

#### typedef

typedef: The typedef is used to give data type a new name. For example,

=) typedef unsigned char preetam; this will rename the type unsigned char as preetam.

there are two ways of typedefing our own custom types :

```cpp

struct Point{
  int x;
  int y;
};
typedef struct Point Point;
// or
typedef struct Point{
  int x;
  int y;
} Point;
```

-> Difference between typedef and #define is that type def only happens at compiletime and also works only on types.

<hr>

### Lambdas :

Whenever we have a function pointer we can use a lambda.

=) auto lambda = [](parameters) {function body};

lambdas can help us make anonymous functions too.
-> the square brackets are actually for taking captures.
-> capture are value that exist in current scope but might not be present when the lambda defined function is called.
-> hence we can use capture to actually mention elements that are in the current scope and available to the function.

```cpp
int a = 12;
auto lambda = [=](int value){ std::cout << a<< std::endl;}; // pass everying by value
auto lambda = [&](int value){ std::cout << a<< std::endl;}; // pass everying by reference
auto lambda = [&a](int value){ std::cout << a<< std::endl;}; // pass a by reference
```

-> we can obviously look into more of this stuff in cppreference.com

<hr>

##### std::find_if :

std::find_if is used just like forEach loop in JS :

we #include < algorithm>

=) auto it = std::find_if(begin_add, end_add, callbackFunction)
-> the callback function must return boolean and accept values that are stored between passed pointer
-> first value that returns true will get its pointer returned.

```cpp
#include<algorithm>

std::vector<int> values = {1,2,3,4,5};
auto it std::find_if(values.begin(), values.end(), [](int value){ return value > 3;});
std::cout << *it <<std::endl;
```

the above code prints : 5
NOTE: this is like the function array.any() in JS.

-> so we are just looping through the list and upon the first element that returns true, we re return a pointer to it.

<hr>

#### Namespaces :

classess are also like namespaces for inner classes or static members.

-> we can have nested namespaces too and accesss them like :

```cpp
using namespace a::b;
```

-> namespaces fix ambiguity issues.
-> we generally specify namespaces inside header files.

we can even do this :

```cpp
namespace a = std;
```

<hr>

#### userinput in CPP :

=) cin.ignore(numeric_limits< streamsize>::max(),'\n'); is used to clear the stream in order to get rid of the \n at the end of the input stream. this is needed when we take input of a number or other type that cannot accept the "\n" and that stays in the buffer. In that case we need to flush the buffer using this.

NOTE: we can do some optimizations when taking userinput in cpp. Thing is, scanf is faster than cinn. and its recomended to use scanf. However!

=) ios_base::sync_with_stdio(false);
=) cin.tie(NULL);

ios_base::sync_with_stdio(false); toggles on or off the synchronization of all the C++ standard streams with their corresponding standard C streams if it is called before the program performs its first input or output operation. Adding ios_base::sync_with_stdio (false); (which is true by default) before any I/O operation avoids this synchronization.

cin.tie(NULL); is a method that simply guarantees the flushing of std::cout before std::cin accepts an input. This is useful for interactive console programs which require the console to be updated constantly but also slows down the program for large I/O. The NULL part just returns a NULL pointer.

IMPORTANT -> It is recommended to use cout << “\n”; instead of cout << endl;. endl is slower because it forces a flushing stream, which is usually unnecessary

HERE IS A TEMPLATE CODE :

```cpp
#include<bits/stdc++.h>
using namespace std;

#define ll long long
#define ar array

void solve(){
    // code here
    cout << ans << "\n";
}
int main(){
    ios_base::sync_with_stdio(0);
    cin.tie(0);

    int t;
    cin>>t;
    while(t--) solve();
}
```
