# Java Questions

1. What are packages in Java?
   
   A package in Java is used to group related classes.
   If you omit the package statement while writing the class definition, the class name is placed into the default package, which has no name.Java compiler automatically imports this package.
   Second, the `java.lang package` is imported implicitly.

2. What is the right data type to represent a price in Java?
   
   If memory is not a concern and performance is not critical, **BigDecimal** will be the right data type represent a price in Java.
   If not, double with predefined precision.

3. What is the size of int in 64-bit JVM?
   
   The size of an int variable is constant in Java, it is always 32-bit regardless of platform. This means the size of primitive int is identical in both 32-bit and 64-bit Java Virtual Machine.

4. How do you identify if JVM is 32-bit or 64-bit from Java Program?
   
   This can be identified by checking some system properties such as sun.arch.data.model or os.arch. (`System.getProperty("sun.arch.data.model") `). Or on cmd line with `java -version`.

5. What is the maximum heap size of 32-bit and 64-bit JVM?
   
   In theory, the maximum heap memory you can assign to a 32-bit JVM is 2^32, which is 4GB, but practically the bounds are much smaller.  
   It also depends on operating systems, e.g. from 1.5GB in Windows to almost 3GB in Solaris.  
   64-bit JVM allows you to stipulate larger heap size, hypothetically 2^64, which is quite large but practically you can specify heap space up to 100GBs.

6. What is the difference among JVM Spec, JVM Implementation, JVM Runtime ?
 
   The JVM spec is the blueprint for the JVM generated and owned by Sun. The JVM implementation is the actual implementation of the spec by a vendor and the JVM runtime is the actual running instance of a JVM implementatio
   
7. Difference between a[] and []a in Java?
    
   You can declare an array in Java by either prefixing or suffixing[] with variable.  
   There is not much difference between them if you are not creating more than one variable in one line, but if you do then it creates different types of variables, as shown in following example :  
    `int a[], b; // first is int array, second is just int variable `  
    `int[] c, d; // both c and d are integer array`

8. Is **String** a datatype in Java?
   
   The interviewer wanted an explanation which stated that String is not a primitive data type in Java; it is one of the most extensively used objects in Java, which is an instance of String class.

9. **String** class is defined under which package in Java?
    
   The answer to this Java question is java.lang package, and this will test the very basics of core Java knowledge.

10. **For-each** loop in Java
    
    ```
    for (type var : array) { 
      statements using var;
    }
    ```
    is equivalent to:
    ```
    for (int i=0; i<arr.length; i++) { 
      type var = arr[i];
      statements using var;
    }
    ```
    Limitations of for-each loop  
    - For-each loops are not appropriate when you want to modify the array.
    - For-each loops do not keep track of index. So we can not obtain array index using For-Each loop 
    - For-each only iterates forward over the array in single steps 
    - For-each cannot process two decision making statements at once 

11. Explain **forEach** function
   
    Java 8 has introduced forEach method in java.lang.Iterable interface so that while writing code we focus on business logic only.  
   For instance, consider a for-loop version of iterating and printing a Collection of Strings:  
      ```
      for (String name : names) {
         System.out.println(name);
      }
      ```
      We can write this using forEach:
      ```
      names.forEach(name -> {
         System.out.println(name);
      });
      ```
      The action to be performed is contained in a class that implements the Consumer interface and is passed to forEach as an argument.

      The `Consumer` interface is a *functional interface* (an interface with a single abstract method). It accepts an input and returns no result.

      Here’s the definition:
      ```
      @FunctionalInterface
      public interface Consumer {
          void accept(T t);
      }
      ```
      Therefore, any implementation, for instance, a consumer that simply prints a String:
      ```
      Consumer<String> printConsumer = new Consumer<String>() {
          public void accept(String name) {
            System.out.println(name);
          };
      };
      ```
      can be passed to forEach as an argument:

      `names.forEach(printConsumer);`
    
       Since Consumer Interface is a functional interface, we can express it in Lambda:  
      `(argument) -> { //body }`.  
      Therefore, our printConsumer is simplified:  
      `name -> System.out.println(name)`  
      And we can pass it to forEach:  
      `names.forEach(name -> System.out.println(name));`

       We can use method reference syntax instead of the normal Lambda syntax, where a method already exists to perform an operation on the class:
    
      `names.forEach(System.out::println);`

       ```
      List<String> names = Arrays.asList("Larry", "Steve", "James");
      names.forEach(System.out::println);
      ```
      ```
      Set<String> uniqueNames = new HashSet<>(Arrays.asList("Larry", "Steve", "James"));
      uniqueNames.forEach(System.out::println);
      ```
      ```
      Queue<String> namesQueue = new ArrayDeque<>(Arrays.asList("Larry", "Steve", "James"));
      namesQueue.forEach(System.out::println);
      ```
      ```
      Map<Integer, String> namesMap = new HashMap<>();
      namesMap.put(1, "Larry");
      namesMap.put(2, "Steve");
      namesMap.put(3, "James");

      namesMap.forEach((key, value) -> System.out.println(key + " " + value));
      ```
      As we can see here, we’ve used a `BiConsumer` to iterate over the entries of the Map:

      `(key, value) -> System.out.println(key + " " + value)`

       Enumerations, Iterators and enhanced for-loop are all **external iterators** (remember the methods iterator(), next() or hasNext()?). In all these iterators, it’s our job to specify how to perform iterations.

      Consider this familiar loop:
      ```
      for (String name : names) {
          System.out.println(name);
      }
      ```
      Although we are not explicitly invoking hasNext() or next() methods while iterating over the list, the underlying code that makes this iteration work uses these methods.       This implies that the complexity of these operations is hidden from the programmer, but it still exists.

      Contrary to an **internal iterator** like `forEach` in which the collection does the iteration itself. Internal iterator like forEach, the method only needs to know what is to be done, and all the work of iterating will be taken care of internally.

12. Difference between **String, StringBuffer and StringBuilder** in Java?
    
   - String is immutable whereas StringBuffer and StringBuilder are mutable classes. It means any change e.g. converting String to upper case or trimming white space will produce another instance rather than changing the same instance.
   - StringBuffer is thread-safe and synchronized whereas StringBuilder is not. That’s why StringBuilder is faster than StringBuffer.
   - String concatenation operator (+) internally uses StringBuffer or StringBuilder class.
   - For String manipulations in a non-multi threaded environment, we should use StringBuilder else use StringBuffer class.

13. How to create **Immutable class in Java**?
    
    Immutable class in java means that once an object is created, we cannot change its content.  
      We can create our own immutable class by following the requirements:  
   - The class must be declared as final so that child classes can’t be created.
   - Data members in the class must be declared private so that direct access is not allowed.
   - Data members in the class must be declared as final so that we can’t change the value of it after object creation.
   - A parameterized constructor should initialize all the fields performing a deep copy so that data members can’t be modified with an object reference.
   - Deep Copy of objects should be performed in the getter methods to return a copy rather than returning the actual object reference)
     ```
     public final class Employee  {
        final String sin;
        public Employee(String sin)   {
           this.sin = sin;    
         }  
         public String getSin(){    
            return sin;    
         }    
      }
     ```    
      **Note**: There should be no setters or in simpler terms, there should be no option to change the value of the instance variable.

     Well, Immutability offers several advantages including **thread-safety, ability to cache and result in more readable multithreading code.**

14. What are wrapper classes in Java?
    
    The wrapper class in Java provides the mechanism to convert primitive into object and object into primitive.      
      Since J2SE 5.0, **autoboxing** and **unboxing** feature convert primitives into objects and objects into primitives automatically. The automatic conversion of primitive into an object is known as autoboxing and vice-versa unboxing.  
      Use of Wrapper classes in Java:  
      - **Change the value in Method**: Java supports only call by value. So, if we pass a primitive value, it will not change the original value. But, if we convert the primitive value in an object, it will change the original value.
      - **Serialization**: We need to convert the objects into streams to perform the serialization. If we have a primitive value, we can convert it in objects through the wrapper classes.
      - **Synchronization**: Java synchronization works with objects in Multithreading.
      - **java.util package**: The java.util package provides the utility classes to deal with objects.
      - **Collection Framework**: Java collection framework works with objects only. All classes of the collection framework (ArrayList, LinkedList, Vector, HashSet, LinkedHashSet, TreeSet, PriorityQueue, ArrayDeque, etc.) deal with objects only.
   
15. What is difference between **FileInputStream** and **FileReader** in Java?
    
    Main difference between FileInputStream and FileReader is that former is used to read binary data while later is used to read text data, which means later also consider character encoding while converting bytes to text in Java.

16. Can you **override static method** in Java?
   
    No, you cannot override static method in Java because they are resolved at compile time rather than runtime. Though you can declare and define static method of same name and signature in child class, this will hide the static method from parent class, that's why it is also known as **method hiding** in Java.

    Static methods are resolved statically (i.e. at compile time) based on the class they are called on and not dynamically as in the case with instance methods which are resolved **polymorphically** based on the runtime type of the object.

17. Difference Between **Method Overriding and Method Hiding**

    If a subclass defines a static method with the same signature as a static method in the superclass, then the method in the subclass hides the one in the superclass. This mechanism happens because the static method is resolved at the **compile time**. Static method bind during the compile time using the **type of reference not a type of object**.

      **Difference Between Method Overriding and Method Hiding in Java**
   - In method overriding both the method in parent class and child class are non-static.
   - In method Hiding both the method in parent class and child class are static.
   - In method Overriding method resolution is done on the basis of the Object type.
   - In method Hiding method resolution is done on the basis of reference type.
   - The version of the overridden instance method that gets invoked is the one in the subclass.
   - The version of the hidden static method that gets invoked depends on whether it is invoked from the superclass or the subclass. 
   - In method overriding, we have the ability to use the “super” keyword to explicitly access superclass methods (super keyword is non-static reference variable we cant use it in static method as we know static methods can only access static members of the class ). Therefore, method overriding does not involve method hiding since the “super” keyword allows us to access and invoke superclass methods when needed.

      **Method hiding** means subclass has defined a **class method** with the same signature as a class method in the superclass. In that case the method of superclass is hidden by the subclass. It signifies that : **The version of a method that is executed will NOT be determined by the object that is used to invoke it**. In fact it will be determined by the *type of reference variable used to invoke the method*.

      ```
      public class Animal {
         public static void foo() {
              System.out.println("Animal");
          }
      }

      public class Cat extends Animal {
         public static void foo() {  // hides Animal.foo()
              System.out.println("Cat");
          }
      }

      Animal.foo(); // prints Animal
      Cat.foo(); // prints Cat

      Animal a = new Animal();
      Animal b = new Cat();
      Cat c = new Cat();
      Animal d = null;

      a.foo(); // should not be done. Prints Animal because the declared type of a is Animal
      b.foo(); // should not be done. Prints Animal because the declared type of b is Animal
      c.foo(); // should not be done. Prints Cat because the declared type of c is Cat
      d.foo(); // should not be done. Prints Animal because the declared type of d is Animal
      ```
      **Method overriding** means subclass had defined an **instance method** with the same signature and return type( including covariant type) as the instance method in superclass. In that case method of superclass is overridden(replaced) by the subclass. It signifies that: **The version of method that is executed will be determined by the object that is used to invoke it**. *It will not be determined by the type of reference variable used to invoke the method.*
      ```
      public class Animal {
          public void foo() {
              System.out.println("Animal");
          }
      }

      public class Cat extends Animal {
          public void foo() { // overrides Animal.foo()
              System.out.println("Cat");
          }
      }

      Animal a = new Animal();
      Animal b = new Cat();
      Cat c = new Cat();
      Animal d = null;

      a.foo(); // prints Animal
      b.foo(); // prints Cat
      c.foo(); // prints Cat
      d.foo(): // throws NullPointerException
      ```
18. What is **covariant method overriding** in Java?

    When we override a parent class method, the name, argument types, and return type of the overriding method in child class has to be exactly the same as that of the parent class method. The overriding method was said to be **invariant** with respect to return type. 

      Java version 5.0 onwards it is possible to have different return types for an overriding method in the child class, but the child’s return type should be a subtype of the parent’s return type. The overriding method becomes **variant** with respect to return type.

      The co-variant return type is based on the **Liskov substitution principle.**

      In covariant method overriding, the overriding method can return the subclass of the object returned by original or overridden method. This concept was introduced in Java 1.5 (Tiger) version and it's very helpful in case original method is returning general type like Object class, because, then by using covariant method overriding you can return more suitable object and **prevent client side type casting**. One of the practical use of this concept is in when you **override the clone() method** in Java.

19. Diamond Problem
   
    The **diamond problem** is an ambiguity that can arise as a consequence of allowing multiple inheritance. It is a serious problem for languages (like C++) that allow for multiple inheritance of state. In Java, however, multiple inheritance is not allowed for classes, only for interfaces, and these do not contain state.

    Talking about Multiple inheritance is when a child class is inherits the properties from more than one parents and the methods for the parents are same (Method name and parameters are exactly the same) then child gets confused about which method will be called. This problem in Java is called the Diamond problem.

20. What is the difference between **Object Oriented Programming and Object Based Programming**?

- Object oriented programming supports all the usual OOP features such as inheritance and polymorphism. It also has no built in objects. ex C#, Java, VB. Net
- Object based programming does not support inheritance or polymorphism and does have some built in objects. ex. Javascript, VB

21. How do you **prevent a method from being overridden**?
   
    To prevent a specific method from being overridden in a subclass, use the **final** modifier on the method declaration, which means "this is the final implementation of this method", the end of its inheritance hierarchy.

22. Can a class be declared as **protected**?
   
    The protected access modifier cannot be applied to class and interfaces. Methods, fields can be declared protected, however methods and fields in a interface cannot be declared protected.

23. Does Java have **friend** concept?
   
    Using friend function you can access private members of class. It can be used in C++ not in java. ... In object-oriented programming, a friend function, that is a "friend" of a given class, is a function that is given the same access as methods to private and protected data. Can be achieved in Java by other means, possibly with reflection.

      Package-private (aka. default) is sufficient in most cases where you have a group of heavily intertwined classes. You put your "friends" in the same package.

24. What is **strictfp**?
   
    strictfp is a keyword in java used for restricting floating-point calculations and ensuring same result on every platform while performing operations in the floating-point variable.
Floating point calculations are platform dependent i.e. different output(floating-point values) is achieved when a class file is run on different platforms(16/32/64 bit processors). To solve this types of issue, strictfp keyword was introduced in JDK 1.2 version by following IEEE 754 standards for floating-point calculations.

25. How **JNI** works in Java?

    Java provides the **native** keyword that’s used to indicate that the method implementation will be provided by a native code.  
      Normally, when making a native executable program, we can choose to use static or shared libs:

- Static libs – all library binaries will be included as part of our executable during the linking process. Thus, we won’t need the libs anymore, but it’ll increase the size of our executable file.
- Shared libs – the final executable only has references to the libs, not the code itself. It requires that the environment in which we run our executable has access to all the files of the libs used by our program.  
The latter is what makes sense for JNI as we can’t mix bytecode and natively compiled code into the same binary file.  

   **The native keyword transforms our method into a sort of abstract method:**  
   `private native void aNativeMethod();`  

   With the main difference that **instead of being implemented by another Java class, it will be implemented in a separated native shared library.**

   Java elements:  
  - **“native”** keyword – as we’ve already covered, any method marked as native must be implemented in a native, shared lib.
  - **System.loadLibrary(String libname)** – a static method that loads a shared library from the file system into memory and makes its exported functions available for our Java code.  

   C/C++ elements (many of them defined within jni.h)  
   - JNIEXPORT- marks the function into the shared lib as exportable so it will be included in the function table, and thus JNI can find it
   - JNICALL – combined with JNIEXPORT, it ensures that our methods are available for the JNI framework
   - JNIEnv – a structure containing methods that we can use our native code to access Java elements
   - JavaVM – a structure that lets us manipulate a running JVM (or even start a new one) adding threads to it, destroying it, etc…

