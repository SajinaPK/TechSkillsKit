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

