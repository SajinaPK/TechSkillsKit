C++ Prep Notes

1. **C++ Basics**
   - **Syntax & Data Types**: Review fundamental types, memory allocation (stack vs. heap), and pointers.
   - **Control Structures**: Loops (`for`, `while`), conditional statements (`if`, `switch`), and error handling (`try-catch`).

2. **Object-Oriented Programming (OOP)**
   - **Classes & Objects**: Constructors, destructors, member functions.
   - **Inheritance & Polymorphism**: Virtual functions, overriding, and dynamic dispatch using vtables.
   - **Encapsulation, Abstraction & Access Specifiers**: `public`, `private`, `protected`.
   - **Static Members**: Static variables and methods, their lifecycle and use.

3. **Memory Management**
   - **Smart Pointers**: `std::shared_ptr`, `std::unique_ptr`, and `std::weak_ptr`.
   - **Manual Memory Management**: `new`, `delete`, and potential issues like memory leaks and dangling pointers.
   - **RAII**: Resource acquisition is initialization (use in resource management, file handling).

4. **STL (Standard Template Library)**
   - **Containers**: `std::vector`, `std::list`, `std::set`, `std::map`, and their performance trade-offs.
   - **Iterators**: Different types (`input`, `output`, `bidirectional`, `random access`).
   - **Algorithms**: Sorting, searching, `std::find`, `std::sort`, etc.
   - **Lambda Expressions & Function Objects**: How to use them with STL algorithms.

5. **Concurrency**
   - **Threads**: `std::thread`, thread management (`join`, `detach`).
   - **Synchronization**: Mutex (`std::mutex`), condition variables, and atomic operations.
   - **Futures and Promises**: Asynchronous programming techniques using `std::async`.

6. **Templates**
   - **Function and Class Templates**: Generic programming techniques.
   - **Template Specialization**: Full and partial specialization.
   - **SFINAE (Substitution Failure Is Not An Error)**: Handling edge cases in template instantiations.

7. **C++11/14/17/20 Features**
   - **Move Semantics & Rvalue References**: `std::move`, perfect forwarding, and avoiding unnecessary copies.
   - **Auto & Decltype**: Type inference.
   - **Constexpr**: Compile-time evaluation.
   - **Structured Bindings**: Simplifying multiple return values.

8. **Advanced Topics**
   - **Design Patterns**: Singleton, Factory, Observer, etc.
   - **Multithreading Best Practices**: Lock-free programming, avoiding race conditions, deadlocks.
   - **Memory Profiling and Performance Optimization**: Using tools like Valgrind.
