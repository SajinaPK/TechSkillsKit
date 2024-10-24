1. What is the size of:
2. What is the size of:
3. Explain Padding and Alignment.
4. what is size_t ? why is it used ?
5. What is unique_ptr ? why cant we copy unique_ptr ? how do we do that ?
6. Difference between struct and class

-----------------------------------------------

1. What is the size of:
```
Class A{ 
 int func () {}
};
```
Ans: The class A does not contain any member variables—only a member function func(). In C++, **functions do not contribute to the size of a class object**. Only member variables and certain overhead (like virtual functions) affect the size.

Therefore, the size of an empty class is typically **1 byte**, so that objects can be uniquely addressable in memory. C++ enforces a non-zero size for object uniqueness.

Since A does not have any virtual functions, there’s no virtual table (vtable) involved, which would otherwise increase the size.

2. What is the size of :
```
Class A {
Int *ptr;
Int func() {}
};
```

Ans: This is a pointer to an int. The size of a pointer depends on the architecture:

•	**32-bit system**: The size of a pointer is **4 bytes**.

•	**64-bit system**: The size of a pointer is **8 bytes**.

The function int func() {} is just a member function, which does not affect the size of the class object. In C++, the size of a class only depends on the size of its data members and any virtual function table overhead (if there are virtual functions).

3. Explain Padding and Alignment.

Ans: In C++, **padding** and **alignment** are mechanisms used by compilers to ensure that data members of a class are stored at memory addresses that are optimal for the system's architecture. Misaligned access can cause performance penalties or even crashes on some hardware, so compilers may add **padding bytes** to align data members properly.

Case 1: Simple Class with Different Data Members

```
class A {
    char c; 
    int i;
    double d;
};
```

| Offset  | Member   | Size                           |
|:--------|:---------|:-------------------------------|
|0        |  c       | 1 byte                         |
|1-3      | (padding)| 3 bytes (to align the next int)|
|4        | i        | 4 bytes                        |
|8-11     | (padding)| 4 bytes(to align the next double)
|12       | d        | 8 bytes                        |

**Total Size**:

•	char = 1 byte

•	Padding after char = 3 bytes

•	int = 4 bytes

•	Padding after int = 4 bytes

•	double = 8 bytes

•	Total: 1 + 3 + 4 + 4 + 8 = 20 bytes

However, the compiler might round this up to the nearest multiple of 8 (for optimal **alignment**), making the final size **24 bytes**.

Case 2: Reordering Members to Reduce Padding
```
class A {
    double d;
    int i;
    char c;
};
```

| Offset  | Member  | Size
|---------|---------|-------
| 0       | d       | 8 bytes
| 8       | i       | 4 bytes
| 12      | c       | 1 byte
| 13-15   |(padding)| 3 bytes (to align the class size to a multiple of 8)

•	Total Size:

o	double = 8 bytes

o	int = 4 bytes

o	char = 1 byte

o	Padding = 3 bytes (to align total size to 8 bytes boundary)

o	Total: 8 + 4 + 1 + 3 = 16 bytes

By reordering the members, we have reduced the size of the class **from 24 bytes to 16 bytes**.

Case 3: Complex Case with Virtual Functions
```
class A {
    int i;
    virtual void func() {}
};
```

| Offset  | Member         | Size
|---------|----------------|--------
| 0       | i              | 4 bytes
| 4-7     |(padding)       | 4 bytes (to align vtable pointer)
| 8       | vtable pointer | 8 bytes

Total Size:

•	int = 4 bytes

•	Padding = 4 bytes (to align the vtable pointer)

•	vtable pointer = 8 bytes

•	Total: 4 + 4 + 8 = 16 bytes

You can explicitly control padding using compiler-specific pragmas or attributes like **#pragma pack** to reduce memory usage, but it might result in inefficient memory access.
```
#pragma pack(1)
class A {
    char c;
    int i;
    double d;
};
#pragma pack()
```

| Offset  | Member | Size
|---------|--------|--------
| 0       | c      | 1 byte
| 1       | i      | 4 bytes
| 5       | d      | 8 bytes

•	Total Size:

o	1 + 4 + 8 = 13 bytes (no padding added).

However, packed structures can result in performance penalties because the data might not be aligned to the boundaries the hardware prefers. This can slow down memory access or cause misaligned access errors on some systems.

4. what is size_t ? why is it used ?

Ans: size_t is an unsigned integer type in C and C++ that is used to represent the size of objects in bytes, and it is guaranteed to be big enough to contain the size of any object on the system.

It is defined in the <stddef.h> (for C) or <cstddef> (for C++) headers.

**Platform-Dependent Size:**

•	On a **32-bit system**, size_t is typically 4 bytes (32 bits), allowing it to represent values from 0 to 4,294,967,295.

•	On a **64-bit system**, size_t is typically 8 bytes (64 bits), allowing it to represent values from 0 to 18,446,744,073,709,551,615.

*size_t* is **platform-independent**, meaning that the code can work seamlessly across 32-bit and 64-bit systems. It will adjust to the size required by the platform to store memory sizes.

1.	With sizeof(): sizeof returns the size of an object or data type in bytes, and its return type is size_t.

`size_t sizeOfInt = sizeof(int);  // sizeOfInt will be platform-dependent`

2.	With Memory Management Functions: Functions like malloc, calloc, and realloc take size_t as an argument because they allocate memory based on the size of objects.

`int* arr = (int*)malloc(10 * sizeof(int));  // malloc takes a size_t argument`

3.	With String Length Functions: Functions like strlen return the length of a string as a size_t value because the length is always non-negative.

```
const char* str = "Hello";
size_t len = strlen(str);  // length of the string returned as size_t
```

4.	With STL Containers: Many functions and methods in the Standard Template Library (STL) use size_t for sizes, such as std::vector::size() or std::string::length(), because these sizes represent the number of elements or characters, which cannot be negative.
```
std::vector<int> vec = {1, 2, 3, 4, 5};
size_t vecSize = vec.size();  // returns the size of the vector as size_t
```
5. What is unique_ptr ? why cant we copy unique_ptr ? how do we do that ?

Ans: *std::unique_ptr* is a smart pointer provided by the C++ Standard Library that **manages the lifetime of dynamically allocated objects**. It ensures that the object it owns is **automatically destroyed** (i.e., its memory is deallocated) when the unique_ptr goes out of scope. It uses RAII (Resource Acquisition Is Initialization) principles. This makes it useful for resource management, as it prevents memory leaks.

The **exclusive ownership** model of std::unique_ptr prohibits copying. If you were able to copy a unique_ptr, two different smart pointers would both try to delete the same object, leading to **double deletion**, which causes undefined behavior.
```
std::unique_ptr<int> p1 = std::make_unique<int>(10);
// std::unique_ptr<int> p2 = p1; // Error: unique_ptr cannot be copied
```
Instead of copying, ownership can be transferred using move semantics. This is done with *std::move()*:

```
std::unique_ptr<int> p1 = std::make_unique<int>(10);  // p1 owns the memory
std::unique_ptr<int> p2 = std::move(p1);  // Ownership transferred to p2

if (!p1) {
    std::cout << "p1 is now nullptr" << std::endl;  // p1 no longer owns the memory
}
std::cout << *p2 << std::endl;  // Outputs 10
```

6. Difference between struct and class

Ans: The primary difference between struct and class in C++ comes down to **default access control** and **intended use**, but both are very similar and can be used interchangeably in most cases.

**Private by default**: All members (data and methods) of a class are private unless explicitly specified otherwise.

```
class MyClass {
    int a;  // Private by default
public:
    void func() {}  // Public
};
```

**Public by default**: All members (data and methods) of a struct are public unless explicitly specified otherwise.

```
struct MyStruct {
    int a;  // Public by default
    void func() {}  // Public
};
```

A class is typically used when you want to encapsulate data and behavior, often adhering to **object-oriented programming (OOP)** principles like **encapsulation, inheritance, and polymorphism**

A struct is typically used for simple data structures that hold just data without much behavior (though this is not a hard rule in C++).

Both class and struct support inheritance, but their default access levels affect how members are inherited.

```
class Base {};
class Derived : Base {};  // Private inheritance
struct Base {};
struct Derived : Base {};  // Public inheritance
```

In C++, struct is more commonly used in situations where C compatibility is needed, since struct is part of the C programming language, whereas class is not. Both can have constructors, destructors, methods, static members, etc.

```
class MyClass {
    int x;  // Private by default
public:
    MyClass(int value) : x(value) {}
    int getValue() { return x; }
};

struct MyStruct {
    int x;  // Public by default
    MyStruct(int value) : x(value) {}
    int getValue() { return x; }
};
```
