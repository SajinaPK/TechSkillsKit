1. **What are the advantages of NumPy over regular Python lists?**

    NumPy is the fundamental package for scientific computing in Python. 
    - Numpy arrays consume less memory. 
    - Numpy arrays take less time to perform the operations on arrays than lists.
    - Numpy arrays are convenient to use as they offer simple array multiple, addition, and a lot more built-in functionality.

    **List**
    - **Element Overhead**: Lists in Python store additional information about each element, such as its type and reference count. This overhead can be significant when dealing with a large number of elements.
    - **Datatype**: Lists can hold different data types, but this can decrease memory efficiency and slow numerical operations. The list can be homogeneous or heterogeneous.
    - **Memory Fragmentation**: Lists may not store elements in contiguous memory locations, causing memory fragmentation and inefficiency.
    - **Performance**: Lists are not optimized for numerical computations and may have slower mathematical operations due to Python’s interpretation overhead. They are generally used as general-purpose data structures.
    - **Functionality**: Lists can store any data type, but lack specialized NumPy functions for numerical operations.

    **Numpy Arrays**
    - **Homogeneous Data**: NumPy arrays store elements of the same data type, making them more compact and memory-efficient than lists.
    - **Fixed Data Type**: NumPy arrays have a fixed data type, reducing memory overhead by eliminating the need to store type information for each element.
    - **Contiguous Memory**: NumPy arrays store elements in adjacent memory locations, reducing fragmentation and allowing for efficient access.
    - **Array Metadata**: NumPy arrays have extra metadata like shape, strides, and data type. However, this overhead is usually smaller than the per-element overhead in lists.
    - **Performance**: NumPy arrays are optimized for numerical computations, with efficient element-wise operations and mathematical functions. These operations are implemented in C, resulting in faster performance than equivalent operations on lists.

    Element-wise operation is not possible on the list. Python list is by default 1-dimensional. But we can create an N-Dimensional list. But then too it will be 1 D list storing another 1D list

    Element-wise operation is possible in Numpy.array(). We can create an N-dimensional array in Python using Numpy.array().

2. **What is monkey patching in Python?**

    The term monkey patch refers to dynamic (or run-time) modifications of a class or module. In Python, we can actually change the behaviour of code at run-time.

    ```
    class monkey:
      def patch(self):
        print ("patch() is being called")

    def monk_p(self):
      print ("monk_p() is being called")

    # replacing address of "patch" with "monk_p"
    monkey.patch = monk_p

    obj = monkey()

    obj.patch()
    # monk_p() is being called
    ```

3. **What are Access Specifiers in Python?**

    Python uses the ‘_’ symbol to determine the access control for a specific data member or a member function of a class. A Class in Python has three types of Python access modifiers:

    - **Public Access Modifier**: All data members and member functions of a class are public by default. 
    - **Protected Access Modifier**: All data members of a class are declared protected by adding a single underscore ‘_’ symbol before the data members of that class. 
    - **Private Access Modifier**: Data members of a class are declared private by adding a double underscore ‘__’ symbol before the data member of that class.
  
4. **Python Global Interpreter Lock (GIL)?**

    Python Global Interpreter Lock (GIL) is a **type of process lock that is used by Python whenever it deals with processes**. Generally, Python only uses only one thread to execute the set of written statements. The performance of the single-threaded process and the multi-threaded process will be the same in Python and this is because of GIL in Python. **We cannot achieve multithreading in Python because we have a global interpreter lock that restricts the threads and works as a single thread**.

    The Python Global Interpreter Lock or GIL, in simple words, is a mutex (or a lock) that allows only one thread to hold the control of the Python interpreter.

    Python uses **reference counting for memory management**. It means that objects created in Python have a reference count variable that keeps track of the number of references that point to the object.

    The problem was that this reference count variable needed protection from race conditions where two threads increase or decrease its value simultaneously. This reference count variable can be kept safe by adding locks to all data structures that are shared across threads so that they are not modified inconsistently. This can cause another problem — Deadlocks. **The GIL is a single lock on the interpreter itself**. This prevents deadlocks (as there is only one lock) and doesn’t introduce much performance overhead. But it effectively makes any CPU-bound Python program single-threaded.

5. **What are Function Annotations in Python?**

    Function Annotation is a feature that allows you to add metadata to function parameters and return values. This way you can specify the input type of the function parameters and the return type of the value the function returns.

    Function annotations are **arbitrary Python expressions that are associated with various parts of functions**. These expressions are evaluated at **compile time** and have no life in Python’s runtime environment. Python does not attach any meaning to these annotations. They take life when interpreted by third-party libraries, for example, mypy.

    The benefits from function annotations can only be reaped via third party libraries. The type of benefits depends upon the type of the library, for example  
    `def fib(n:'int', output:'list'=[])-> 'list': `

   The function annotations in the above code can be accessed by a special attribute ‘__annotations__’ OR by using standard module ‘pydoc’ OR by using standard module ‘inspect’:  
    `print(fib.__annotations__)`  
    `print(inspect.getfullargspec(fib))`

6. 
