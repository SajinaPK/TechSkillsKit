1. **What are the benefits of using Python language as a tool in the present scenario ?**

    The following are the benefits of using Python language:

  - Object-Oriented Language
  - High-Level Language
  - Dynamically Typed language
  - Extensive support Libraries
  - Presence of third-party modules
  - Open source and community development
  - Portable and Interactive
  - Portable across Operating systems

2. **Is Python a compiled language or an interpreted language?**

    First off, interpreted/compiled is not a property of the language but a property of the implementation. For most languages, most if not all implementations fall in one category, so one might save a few words saying the language is interpreted/compiled too.

    Actually, Python is a **partially compiled language and partially interpreted language**. The compilation part is done first when we execute our code and this will generate byte code internally, this byte code gets converted by the Python virtual machine(p.v.m) according to the underlying platform(machine+operating system).

3. **What is the difference between a Mutable datatype and an Immutable data type?**

  - Mutable data types can be edited i.e., they can change at runtime. Eg – List, Dictionary, etc.
  - Immutable data types can not be edited i.e., they can not change at runtime. Eg – String, Tuple, etc

4. **How are arguments passed by value or by reference in Python?**

    Python’s argument-passing model is **neither “Pass by Value” nor “Pass by Reference” but it is “Pass by Object Reference”**. 

    Depending on the type of object you pass in the function, the function behaves differently. Immutable objects show “pass by value” whereas mutable objects show “pass by reference”.

5. **What is List Comprehension? Give an Example.**

    List comprehension offers a shorter syntax when you want to create a new list based on the values of an existing list.
    `my_list = [i for i in range(1, 10)]`

6. **Differences and Applications of List, Tuple, Set and Dictionary**

| **List**                                                                                                         | **Tuple**                                                                                                          | **Set**                                                                                                  | **Dictionary**                                                                     |
|------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| A list is a non-homogeneous data structure that stores the elements in columns of a single row or multiple rows. | A Tuple is also a non-homogeneous data structure that stores elements in columns of a single row or multiple rows. | The set data structure is also a non-homogeneous data structure but stores the elements in a single row. | A dictionary is also a non-homogeneous data structure that stores key-value pairs. |
|                                        The list can be represented by [ ]                                        |                                          Tuple can be represented by  ( )                                          |                                     The set can be represented by { }                                    |                      The dictionary can be represented by { }                      |
|                                        The list allows duplicate elements                                        |                                           Tuple allows duplicate elements                                          |                                 The Set will not allow duplicate elements                                |                    The dictionary doesn’t allow duplicate keys.                    |
|                                         The list can use nested among all                                        |                                           Tuple can use nested among all                                           |                                     The set can use nested among all                                     |                       The dictionary can use nested among all                      |
| A list is mutable i.e we can make any changes in the list.                                                       | A tuple is immutable i.e we can not make any changes in the tuple.                                                 |A set is mutable i.e we can make any changes in the set, but elements are not duplicated.                 | A dictionary is mutable, but Keys are not duplicated.                              |

7. **What is a lambda function?**

    A lambda function is a small anonymous function.

    A lambda function can take any number of arguments, but can only have one expression.  
    `lambda arguments : expression`  
    `a = lambda x, y : x*y`

8. **What is a pass in Python**

    The pass statement is used as a **placeholder for future code**.

    When the pass statement is executed, nothing happens, but you avoid getting an error when empty code is not allowed.

    Empty code is not allowed in loops, function definitions, class definitions, or in if statements.
    ```
    for x in [0, 1, 2]:
    pass
    ```

9. **What is the difference between / and // in Python?**

    / represents floor division whereas // represents precise division. For Example:

    5//2 = 2  
    5/2 = 2.5

10. **Can we Pass a function as an argument in Python?**

    Yes, Several arguments can be passed to a function, including objects, variables (of the same or distinct data types), and functions. Functions can be passed as parameters to other functions because they are objects. Higher-order functions are functions that can take other functions as arguments.

11. **What are `*args` and `**kwargs`?**

    To pass a variable number of arguments to a function in Python, use the special syntax `*args` and `**kwargs` in the function specification. It is used to **pass a variable-length, keyword-free argument** list. By using the *, the variable we associate with the * becomes iterable, allowing you to do operations on it such as iterating over it and using higher-order operations like map and filter.

    One can think of the **kwargs as being a dictionary that maps each keyword to the value** that we pass alongside it. That is why when we iterate over the kwargs there doesn’t seem to be any order in which they were printed out.

    ```
    def myFun(**kwargs):
      for key, value in kwargs.items():
        print("%s == %s" % (key, value))
 
    myFun(first='Hello', mid='to', last='you!')
    ```
12. **What is Scope in Python?**

    LEGB is an acronym that stands for the four scopes in Python: Local, Enclosing, Global, and Built-in. 
    - **Local** variable: Local variables are those that are initialized within a function and are unique to that function. It cannot be accessed outside of the function.
    - **Enclosing** or Module-level scope: It refers to the global objects of the current module accessible in the program.
    - **Global** variables: Global variables are the ones that are defined and declared outside any function and are not specified to any function.
    - **Built-in** or Outermost scope: It refers to any built-in names that the program can call. The name referenced is located last among the objects in this scope.
   
13. **What is docstring in Python?**

    Python documentation strings (or docstrings) provide a convenient way of associating documentation with Python modules, functions, classes, and methods.

    - **Declaring Docstrings**: The docstrings are declared using ”’triple single quotes”’ or “””triple double quotes””” just below the class, method, or function declaration. All functions should have a docstring.
    - **Accessing Docstrings**: The docstrings can be accessed using the __doc__ method of the object or using the help function.

14. **What is Dictionary Comprehension? Give an Example**

    Dictionary Comprehension is a syntax construction to ease the creation of a dictionary based on the existing iterable.

    For Example: `my_dict = {i:1+7 for i in range(1, 10)}`

15. **How do you floor a number in Python?**

    The Python math module includes a method that can be used to calculate the floor of a number. 

    - `floor()` returns the floor of x i.e., the largest integer not greater than x. 
    - `ceil(x)` returns a ceiling value of x i.e., the smallest integer greater than or equal to x.
   
16. **Is Tuple Comprehension? If yes, how, and if not why?**

    Comprehensions are used in Python to create iterable objects from other iterable objects. 

    Tuple comprehension is not possible in Python because it will end up in a generator, not a tuple comprehension.  
    `newTuple=(element**2 for element in oldTuple)`

    We don’t have tuple comprehension in Python as the parentheses are used for **generator comprehension**. 

    Another reason for the absence of tuple comprehension might be that tuples are **immutable**.

17. **Differentiate between List and Tuple?**

    **List**  
    - Lists are Mutable datatype.
    - Lists consume more memory
    - The list is better for performing operations, such as insertion and deletion.
    - The implication of iterations is Time-consuming

    **Tuple**  
    - Tuples are Immutable datatype.
    - Tuple consumes less memory as compared to the list
    - A Tuple data type is appropriate for accessing the elements
    - The implication of iterations is comparatively Faster

18. **What is the difference between a shallow copy and a deep copy?**

| **Shallow Copy**                                                                              | **Deep Copy**                                                                                |
|-----------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
|        Shallow Copy stores the references of objects to the original memory address.          |                        Deep copy stores copies of the object’s value.                        |
|      Shallow Copy reflects changes made to the new/copied object in the original object.      |    Deep copy doesn’t reflect changes made to the new/copied object in the original object.   |
| Shallow Copy stores the copy of the original object and points the references to the objects. | Deep copy stores the copy of the original object and recursively copies the objects as well. |
|                                   A shallow copy is faster.                                   |                              Deep copy is comparatively slower.                              |

19. **What are First Class Objects**

    In Python, **functions are first class objects** which means that functions in Python can be used or passed as arguments.

    Properties of first class functions:
    - A function is an instance of the Object type.
    - You can store the function in a variable.
    - You can pass the function as a parameter to another function.
    - You can return the function from a function.
    - You can store them in data structures such as hash tables, lists
   
20. **What are Decorators?**

    Decorators are used to modify the behaviour of function or class. In Decorators, functions are taken as the argument into another function and then called inside the wrapper function.

    ```
    def decor1(func): 
      def inner(): 
        x = func() 
        return x * x 
    return inner 
 
    def decor(func): 
      def inner(): 
        x = func() 
        return 2 * x 
    return inner 
 
    //decor1(decor(num))
    @decor1
    @decor
    def num(): 
      return 10

    //decor(decor1(num2)) 
    @decor
    @decor1
    def num2():
      return 10
   
    print(num()) 
    print(num2())
    ```
    400  
    200

21. **How do you debug a Python program?**

    By using this command we can debug a Python program:

    `$ python -m pdb python-script.py`

22. **Does Python supports multiple Inheritance?**

    Python does support multiple inheritances, unlike Java. Multiple inheritances mean that a class can be derived from more than one parent class.

23. **How is memory management done in Python?**

    Python uses its private heap space to manage the memory. Basically, all the objects and data structures are stored in the private heap space. Even the programmer cannot access this private space as the interpreter takes care of this space. Python also has an **inbuilt garbage collector**, which recycles all the unused memory and frees the memory and makes it available to the heap space.
    
    There are two parts of memory:
    - **stack memory**
    - **heap memory**  
    
    The methods/method calls and the references are stored in stack memory and all the values objects are stored in a private heap.

24. **How to delete a file using Python?**

    We can delete a file using Python by following approaches:

    - os.remove()
    - os.unlink()

25. **What are Generators in Python?**

    In Python, the **generator is a way that specifies how to implement iterators**. It is a normal function except that it yields expression in the function. It does not implement __itr__ and next() method and reduces other overheads as well.

    A generator function in Python is defined like a normal function, but whenever it needs to generate a value, it does so with the `yield` keyword rather than return. **If the body of a def contains yield, the function automatically becomes a Python generator function**. 

    The `yield` keyword pauses the current execution by saving its states and then resumes from the same when required.

    ```
    def simpleGeneratorFun(): 
      yield 1            
      yield 2            
      yield 3            
   
    # Driver code to check above generator function 
    for value in simpleGeneratorFun():  
      print(value)
    # x is a generator object 
    x = simpleGeneratorFun()
    # In Python 3, __next__() 
    print(next(x)) 
    print(next(x)) 
    print(next(x))
    ```
26. **What is Python Generator Expression?**

    Generator expression is another way of writing the generator function. It uses the Python list comprehension technique but instead of storing the elements in a list in memory, it creates generator objects.

    `(expression for item in iterable)`

    ```
    # generator expression 
    generator_exp = (i * 5 for i in range(5) if i%2==0) 
  
    for i in generator_exp: 
      print(i)
    ```
27. **What is PIP?**

    PIP is an acronym for **Python Installer Package** which provides a seamless interface to install various Python modules. It is a command-line tool that can search for packages over the internet and install them without any user interaction.

28. **What is a zip function?**

    Python `zip()` function returns a zip object, which maps a similar index of multiple containers. It takes an iterable, converts it into an iterator and aggregates the elements based on iterables passed. It returns an iterator of tuples.

    ```
    a = ("John", "Charles", "Mike")
    b = ("Jenny", "Christy", "Monica")

    x = zip(a, b)
    ```
29. **What is `__init__()` in Python?**

    Equivalent to constructors in OOP terminology, `__init__` is a reserved method in Python classes. The `__init__` method is called automatically whenever a new object is initiated. This method allocates memory to the new object as soon as it is created. This method can also be used to initialize variables.

30. **What are Pickling and Unpickling?**

    **Pickling** is the Python term for serializing an object, which entails **transforming it into a binary representation that can be stored in a file or communicated over a network**. Python has built-in functions for the pickling objects in the pickle module.

    **Deserializing a pickled object entails turning it from its binary representation** back to a Python object that can be used in code. This process is known as **unpickling**.

    ```
    import pickle

    # Define a Python object
    person = {
      "name": "Alice",
      "age": 30,
      "gender": "female"
    }
 
    # Pickle the object to a binary file
    with open("person.pickle", "wb") as file:
      pickle.dump(person, file)

    # Binary file named ‘person.pickle’ will be created in the same directory
    print("Pickling completed")

    # load the data from a file
    with open('data.pkl', 'rb') as f:
      data = pickle.load(f)
 
    # print the data
    print(data)
    ```
