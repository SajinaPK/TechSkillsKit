1. What is **Circuit Breaker**?
  
   The Circuit Breaker pattern is a design pattern used to **handle faults, failures, and latency in distributed systems**. It involves three states: **closed** (normal operation), **open** (blocking requests due to failures), and **half-open** (allowing a limited number of requests to check for recovery). The pattern improves fault tolerance and prevents cascading failures.
  
   Circuit Breaker allows **graceful handling of failed remote services**. It's especially useful when all parts of our application are highly decoupled from each other, and failure of one component doesn't mean the other parts will stop working.
   
   Circuit breaker is a design pattern used in modern software development. It is used to detect failures and encapsulates the logic of preventing a failure from constantly recurring, during maintenance, temporary external system failure or unexpected system difficulties.
    
   Spring Cloud Circuit Breaker supports many different circuit breaker implementations including, Resilience4J, Hystrix, Sentinal, and Spring Retry.

2. Can you provide an **example of the Circuit Breaker pattern** in Java using Netflix Hystrix?
  
   Here’s a simplified example using Netflix Hystrix:
   ```
   @HystrixCommand(fallbackMethod = "fallbackMethod")
      public String invokeExternalService() {
      // Code to invoke the external service
    }
    public String fallbackMethod() {
      // Fallback logic when the circuit is open
    }
    ```
   In this example, the `@HystrixCommand` annotation is used to wrap the method that invokes the external service, and a fallback method is provided for handling failures when the circuit is open.

3. How long does heap memory and stack memory live in Java?
  
   **Heap Memory**: Objects in heap memory can live for the duration of the program or until they are no longer reachable and become eligible for garbage collection.  
   **Stack Memory**: The lifetime of data in stack memory is short-lived, tied to the duration of method calls. Each method call gets its own frame on the stack, and frames are created and destroyed as methods are called and return.

4. What is the difference between an **Abstract class** and an **Interface?**
  
   An abstract class can have both abstract and non-abstract methods, and it can have variables.  
   An interface can only have abstract methods and final variables (constants).  
   An abstract class can provide a default implementation of methods, while an interface can’t.  
   A class can extend one abstract class, but it can implement multiple interfaces.

5. Explain the difference between **final, finally, and finalize**?.
  
   **Final**:
   The final keyword is used to restrict the user. It can be used in many contexts such as variable, method, and class. Once a final variable has been assigned, it always contains the same value. If a final method is inherited from a class, then it cannot be overridden by any subclass, and a final class can’t be inherited.

   **Finally**:
   Finally is a block of code that follows a try block. A finally block of code always executes, whether or not an exception has occurred. Using a finally block allows you to run any cleanup-type statements that you want to execute, no matter what happens in the protected code.

   **Finalize**:
   Finalize is a method that the garbage collector always calls just before the deletion/destroying the object which is eligible for garbage collection, to give it a ‘last chance’ to clean up its resources.

6. What is **Upcasting and Downcasting**?
  
   Upcasting and downcasting are two important concepts in Java, especially when dealing with inheritance and polymorphism.

   **Upcasting** is the process of casting a subclass or derived class to a superclass or base class. In Java, upcasting is always allowed, and it is safe because the subclass has all the properties of its superclass. It’s a way to generalize classes.

   **Downcasting**, on the other hand, is the casting from a superclass to a subclass. This is not directly allowed in Java, because the superclass does not have all the properties of the subclass, and it can be risky. To downcast, you must explicitly write the subclass type in parentheses, like so:  
   `BaseClass obj1 = (DerivedClass) obj2; // Downcasting`

7. Can we **reduce the accessibility of parent class member** in child class?
  
   In short, you cannot directly reduce the accessibility of a member in a child class below what was in the parent class.Access modifiers determine the level of visibility and access and they can only be equal to or more permissive in the child class compared to the parent class.

8. The difference between **encapsulation and abstraction**?
  
    **Encapsulation** is concerned with hiding the internal state and restricting access to the internal details of an object. **Information hiding.**.   
   It is the packing of "data" and "functions operating on that data" into a single component and restricting the access to some of the object's components.

   **Abstraction** is concerned with simplifying complex systems by emphasizing the essential features of an object and hiding unnecessary details. **Implementation hiding.**  
   It is a mechanism which represent the essential features without including implementation details.

   In real world, encapsulation and abstraction often go hand in hand, as encapsulation helps achieve abstraction by hiding implementation details.

9. What is **coupling**?
   
    "coupling" pertains to the level of **interdependence among various classes** or modules in a program, illustrating the extent to which one class or module depends on another. In software design, the common objective is to strive for low coupling, as it enhances the modularity, maintainability, and flexibility of the code.

10. Explain more about **try with resource**?
   
    In Java, the **“try-with-resources”** statement streamlines the management of resources, particularly when working with objects that adhere to the `AutoCloseable` or `Closeable` interfaces. Objects like **file streams, network connections, or database connections** must be explicitly closed after usage to release system resources. The try-with-resources statement simplifies this process by automatically ensuring that the resources are appropriately closed, even in the event of an exception.
     ```
     import java.io.FileInputStream;
     import java.io.IOException;

     class TryWithResource {
      public static void main(String[] args) {
      // Using try-with-resources with FileInputStream
      try (FileInputStream fis = new FileInputStream("sample.txt")) {
         // Code that uses the FileInputStream
       } catch (IOException e) {
         // Exception handling
         e.printStackTrace();
       }
      }
     }
     ```
11. **Exception vs Error**?
   
    **Exceptions** in Java represent conditions that a program might want to catch and handle. They are used for scenarios that are considered recoverable, meaning the program can take corrective action and continue running. Ex  `FileNotFoundException`

    **Errors** in Java represent serious issues that are usually beyond the control of the application. They often indicate problems at a system level or issues with the underlying hardware. Ex `OutOfMemoryError`

12. What is **method reference** in java?
   
    In Java, method reference is a shorthand notation that allows you to refer to methods or constructors without invoking them. It is a syntactic sugar for lambda expressions. Method references are often used to make the code more concise and readable. Exa: `System.out::println`

    Notice that method references always utilize the :: operator.

    There are four kinds of method references:
    - Static methods
    - Instance methods of particular objects
    - Instance methods of an arbitrary object of a particular type
    - Constructor

     **Example 1**:  
    `List<String> messages = Arrays.asList("hello", "baeldung", "readers!");`  
     We can achieve this by leveraging a simple lambda expression calling the `StringUtils.capitalize()` method directly:
     `messages.forEach(word -> StringUtils.capitalize(word));`  
     Or, we can use a method reference to simply refer to the capitalize static method:  
     `messages.forEach(StringUtils::capitalize);`

     **Example 2**:
      ```
      public class Bicycle {
        private String brand;
        private Integer frameSize;
        // standard constructor, getters and setters
      }
      public class BicycleComparator implements Comparator {
        @Override
        public int compare(Bicycle a, Bicycle b) {
          return a.getFrameSize().compareTo(b.getFrameSize());
        }
      }
      ```

      `BicycleComparator bikeFrameSizeComparator = new BicycleComparator();`

      We could use a lambda expression to sort bicycles by frame size, but we’d need to specify two bikes for comparison:  
      `createBicyclesList().stream().sorted((a, b) -> bikeFrameSizeComparator.compare(a, b));`  

      Instead, we can use a method reference to have the compiler handle parameter passing for us:  
      `createBicyclesList().stream().sorted(bikeFrameSizeComparator::compare);`  

      **Example 3**:  
      `List<Integer> numbers = Arrays.asList(5, 3, 50, 24, 40, 2, 9, 18);`  
      If we use a classic lambda expression, both parameters need to be explicitly passed, while using a method reference is much more straightforward:  
      ```
      numbers.stream().sorted((a, b) -> a.compareTo(b));
      numbers.stream().sorted(Integer::compareTo);
      ```

      **Example 4**:  
      `List<String> bikeBrands = Arrays.asList("Giant", "Scott", "Trek", "GT");`
      ```
      public Bicycle(String brand) {
        this.brand = brand;
        this.frameSize = 0;
      }
      ```

      `bikeBrands.stream().map(Bicycle::new).toArray(Bicycle[]::new);`

      Notice how we called both Bicycle and Array constructors using a method reference, giving our code a much more concise and clear appearance.  
      [The overall result of the above line is an array of Bicycle objects, each with a brand taken from the original list of bikBrands.]

      **Limitation**
      One main limitation is a result of what’s also their biggest strength: the output from the previous expression needs to match the input parameters of the referenced method signature.

      Let’s see an example of this limitation:
      ```
      createBicyclesList().forEach(b -> System.out.printf(
        "Bike brand is '%s' and frame size is '%d'%n",
        b.getBrand(),
        b.getFrameSize()));
      ```
      This simple case can’t be expressed with a method reference, because the printf method requires 3 parameters in our case, and using createBicyclesList().forEach() would only allow the method reference to infer one parameter (the Bicycle object).

13. What **New Features Were Added in Java 8**?
   
    Java 8 ships with several new features, but the most significant are the following:

    - **Lambda Expressions** − a new language feature allowing us to treat actions as objects
    - **Method References** − enable us to define Lambda Expressions by referring to methods directly using their names
    - **Optional** − special wrapper class used for expressing optionality
    - **Functional Interface** – an interface with maximum one abstract method; implementation can be provided using a Lambda Expression
    - **Default methods** − give us the ability to add full implementations in interfaces besides abstract methods
    - **Nashorn, JavaScript Engine** − Java-based engine for executing and evaluating JavaScript code
    - **Stream API** − a special iterator class that allows us to process collections of objects in a functional manner
    - **Date API** − an improved, immutable JodaTime-inspired Date API
   
14. Describe Some of the **Functional Interfaces** in the Standard Library
   
    There are a lot of functional interfaces in the java.util.function package. The more common ones include, but are not limited to:
    - *Function* – it takes one argument and returns a result
    - *Consumer* – it takes one argument and returns no result (represents a side effect)
    - *Supplier* – it takes no arguments and returns a result
    - *Predicate* – it takes one argument and returns a boolean
    - *BiFunction* – it takes two arguments and returns a result
    - *BinaryOperator* – it is similar to a BiFunction, taking two arguments and returning a result. The two arguments and the result are all of the same types.
    - *UnaryOperator* – it is similar to a Function, taking a single argument and returning a result of the same type

15. What is a **Stream**?
   
    In simple terms, a stream is an iterator whose role is to accept a set of actions to apply on each of the elements it contains.

    The stream represents a sequence of objects from a **source** such as a collection (like a list or a set), an array, an I/O channel, or even just a generator function, which **supports aggregate operations**.

    **Intermediate Operations**: These are operations that transform a stream into another stream. Examples include map(), filter(), flatMap(), distinct(), sorted(), peek(), limit(), skip(). They are lazy, meaning they don't execute until a terminal operation is invoked  
    `Stream<Integer> filteredStream = stream.filter(n -> n % 2 == 0);`

    **Terminal Operations**: These operations produce a result or a side-effect. Examples include toArray(), collect(), count(), reduce(), forEach(), min(), max(), anyMatch(), forEachOrdered(), allMatch(), noneMatch(), findAny(), findFirst(). Once a terminal operation is called, the stream is consumed and cannot be reused  
    filteredStream.forEach(System.out::println);

16. Find the **first non-repeating characters** in a given String?

    ```
    String input = "Hello World! How are you?"
    input.chars() //gives you the source as a stream
    
    //convert each primitive char to a Character object, allowing you to work with a stream of objects
    input.chars().mapToObj(ch->(char) ch)
    
    // find the occurrence of each character in the string: returns you HashMap<Character, Long>
    input.chars()
      .mapToObj(ch->(char) ch)
      .collect(Collectors.groupingBy(Character::toLowerCase, Collectors.counting())
    ```
    ```
    Optional<Character> first = input.chars()
        .mapToObj(ch->(char) ch)
        .collect(Collectors.groupingBy(Character::toLowerCase, Collectors.counting())
        .entrySet().stream() //take the entry set of the hash map and convert to stream source
        .filter(entry->entry.getValue() == 1) //filters out the map value whose occurrence is 1
        .map(Map.Entry::getKey) //get the key ie., the character with 1 occurence
        .findFirst() //get the first find //its a terminal operation and returns an optional character

    // we can use the optional to verify if the value is found or not:
    if (first.isPresent())
      System.out.println(first.get());
    else
      System.out.println("No value found");
    ```

17. Removing duplicate characters from a given String

    ```
    public static String removesDuplicateFromString(String input){

      return input.chars() // converts the string to an IntStream of character values
                .distinct()  // removes duplicates
                .mapToObj(ch -> String.valueOf((char) ch))  //converts each character back to a string
                .collect(Collectors.joining());  // concatenates the distinct characters into a new string.
    }
    ```

18. Find the sum of all integers in an array
  
    ```
    int sum = numbers.stream().reduce(0, (a, b) -> a + b);
    OR
    int sum = Arrays.stream(numbers).sum();
    ```
    The reduce operation is used to combine the elements of the stream into a single result. The parameters passed to reduce are:
    - 0: The identity value or initial value for the sum. In this case, it's 0.
    - (a, b) -> a + b: The binary operator that takes two elements and produces a single result. In this case, it's a lambda expression that adds two integers.

    Ex int product = numbers.stream().reduce(1, (a, b) -> a * b);
    The 1 is the initial value for the product, and the lambda expression (a, b) -> a * b multiplies two integers.

19. In Java What Is **Optional**? How Can It Be Used?
   
    In Java, **Optional** is a container class introduced in Java 8 to represent an optional (nullable) value. It is designed to handle scenarios where a value may or may not be present. The primary goal of Optional is to eliminate the need for using null references and to provide a more expressive way to handle the absence of a value.

    **Creating an Optional**:
    - Optional.of(value): Creates an Optional containing the specified non-null value.
    - Optional.ofNullable(value): Creates an Optional containing the specified value, or an empty Optional if the value is null.
    - Optional.empty(): Creates an empty Optional with no value.

    **Accessing the Value**:
    - get(): Retrieves the value if it is present. Note that using get() on an empty Optional will throw a NoSuchElementException.
    - orElse(defaultValue): Retrieves the value if present, or returns a default value if the value is not present.
    - orElseGet(supplier): Retrieves the value if present, or invokes the supplier and returns the result if the value is not present.
    - orElseThrow(exceptionSupplier): Retrieves the value if present, or throws an exception provided by the supplier if the value is not present.

    **Functional Operations**:
    - map(function): Applies a function to the value inside the Optional if it is present.
    - filter(predicate): If a value is present, and it satisfies the given predicate, return an Optional describing the value, otherwise return an empty Optional.
    - flatMap(function): Applies a function to the value inside the Optional if it is present, and flattens the result.  
    ```
    import java.util.Optional;

    public class OptionalExample {
        public static void main(String[] args) {
            // Creating Optional with a value
            Optional<String> optionalValue = Optional.of("Hello, Optional!");

            // Accessing the value
            String result = optionalValue.orElse("Default Value");
            System.out.println(result);

            // Example of map
            String upperCaseValue = optionalValue.map(String::toUpperCase).orElse("No value");
            System.out.println(upperCaseValue);
        }
    }
    ```
20. What is a **Functional Interface**? What Are the Rules of Defining a Functional Interface?
   
    A functional interface is an interface with one **single abstract method** (default and static methods do not count), no more, no less.

    Where an instance of such an interface is required, a Lambda Expression can be used instead. More formally put: **Functional interfaces provide target types for lambda expressions and method references.**

    The arguments and return type of such an expression directly match those of the single abstract method.

    For instance, the Runnable interface is a functional interface, so instead of:
    ```
    Thread thread = new Thread(new Runnable() {
      public void run() {
        System.out.println("Hello World!");
      }
    });
    ```
    We could simply do:  
    `Thread thread = new Thread(() -> System.out.println("Hello World!"));`

    Functional interfaces are usually annotated with the `@FunctionalInterface` annotation, which is informative and doesn’t affect the semantics.

    ```
    @FunctionalInterface
    interface MyFunctionalInterface {
        void myAbstractMethod(); // Single abstract method

        default void myDefaultMethod() {
          System.out.println("Default method implementation");
        }

        static void myStaticMethod() {
          System.out.println("Static method implementation");
        }
    }
    ```
    The main utility of functional interfaces is to provide a target type for lambda expressions and method references.

21. What is a **Default Method** and When Do We Use It?
   
    A default method provides a default implementation for a method in an interface.

    Default methods are often used to add new methods to interfaces without forcing all implementing classes to provide an implementation immediately.  
    They are useful when evolving existing codebases without breaking compatibility.

22. **Java 21 New features**

    1\. Language Feature
      - Unnamed Patterns and Variables  
        You can use **unnamed patterns** in switch expressions and statements:  
        ```
        for (int id : orderIDs) {
          total++;
        }
        ```
        You can use an unnamed variable to elide the unused variable id (underscore keyword _): 
        ```
        for (int _ : orderIDs) {
	        total++;
        }
        ```
        **Unnamed Variables**
        ```
        try (var _ = new FileReader(path)) {
	        // Do nothing
        } catch (IOException e) {
          e.printStackTrace();
        }
        ```
        ```
        try {
	        int i = Integer.parseInt(s);
          System.out.println(i + " is valid");
        } catch (NumberFormatException _) {
          System.out.println(s + " isn't valid");
        }
        ```
      - String Templates
        ```
        String user = "Duke";   
        char option = 'b';
        String choice  = STR."\{user} has chosen option \{option}";
        System.out.println(choice);
        ```

      - It is updated with the ‘pattern matching’ in switch cases, now the developer will be able to match the patterns directly instead of checking the conditions.

      - The Language feature holds the record patterns like enhanced the pattern matching for the switch expressions and the statements.

    2\. Libraries Improvements
      - Virtual threads: JDK 21 has introduced virtual threads to the Java platform, where as they can do tasks quickly without allocating much resources and space in the memory.
      - Sequenced collections: Java 21 has introduced new ways to work with collections, which is an interface to represent collections in a set of order, where the developer will always get to know which item is first, second, third, and so on.
      - Key encapsulation mechanisms (KEMs): JDK 21 has introduced an API for key encapsulation mechanisms (KEM), this tool will help in storing secret keys safely.
      - Vector API: Java 21 offers an API and vector tools which will help you to get fastest performance in such tasks like graphics rendering, or scientific calculations.

    3\. Performance Improvements
      - Java has the feature of Z Garbage Collection (ZBC) which performs all the expensive works concurrently, without stopping the execution of application threads.
        
    4\.  Tools Improvements
      - Java 21 has enhanced its tools such as ‘Runtime.exec’ and ‘ProcessBuilder’ which are used to start new processes like running a new program.

    5\. Java Emoji Support Tools
      - Java has introduced the method in the ‘java.lang.Character’ class to work with different types of emoji’s properties, it’s defined by the Unicode Standard (unicode emoji technical standard) UTS#51.

    6\. Enhanced Lifecycle Management with HttpClient
      - The ‘HttpClient’ being ‘AutoCloseable’ means you can now use it within a try-with-resources block in Java, which automatically handles the closing of resources once they are no longer needed.

    7\. Enhanced Repeated Appending in StringBuilder and StringBuffer
      - JDK 21 has added methods to ‘java.lang.StringBuilder’ and ‘java.lang.StringBuffer’.
        ```
        StringBuilder sb1 = new StringBuilder(); 
        sb1.repeat(42, 10);  // Appends "**********" to sb1
        ```
    8\. Advancing Java collections with Sequenced Interface
      - The JDK 21 version brings new interfaces to the Java collections framework which is enhancing the collection framework and providing the clear sequence order.
      - Consider a queue where you might want to inspect or pull from either the front or the back. With enhanced methods, you can easily get or remove elements from both ends.

23. **Java 17 Features**

    1\.  Nice developer-related features
      - **Switch Pattern Matching** (Preview) - It makes switch statements and expressions more flexible and expressive by letting patterns appear in case labels. It also makes it possible to relax the switch's null-hostility when needed.
      - **Generate sealed Classes** - Sealing allows classes and interfaces to define their permitted subtypes. In other words, a class or an interface can now define which classes can implement or extend it.

    2\. Developer-specific information or features
      - **Restore or Rebuild the "Always-Strict Floating-Point**" Semantics - Both default floating-point operations, strict or strictfp, provide the same outcomes for calculations using floating-point on every platform.
      - **Vector API** (Second Incubator) - The Vector API works with Single Instruction, Multiple Data / SIMD operations, which include multiple sets of instructions being processed concurrently. It uses specialized CPU hardware that provides vector instruction and enables the operation of these instructions as pipelines.
      - **Deserialization Filters Based on Context** (content-specific) - The JDK 9 version makes it possible for us to verify receiving serialized data from untrusted sources, which is a frequent source of security problems. Applications can configure dynamically chosen and context-specific deserialization filters.
      - **Enhanced faster the "pseudo-Random" Number Generators** - It offers a new interface type and solutions for pseudo-random number generators to make using multiple PRNG algorithms simpler and properly support stream-based operations.
      - **JDK Internals Encapsulate strongly**
      - **Foreign Functions and Memory API** (Incubator) - Java programmers can retrieve code from outside the JVM. Thanks to the Foreign Function and Memory API, it controls memory outside of the heap.
        The intention is to replace the JNI API and enhance its performance and security over the previous version.

    3\. **Keeping current with Apple-related features**
      - New macOS rendering pipelines
      - macOS/AArch64 Port

    4\.  **Cleaning up various features**
      - Dismiss the Applet API for Removal - Most browsers will no longer support the applet API because it has been deprecated since JDK9.
      - Activation of the Removal RMI
      - Removal of the Experimental AOT and JIT Compiler
      - Remove the Security Manager.
   
  24. Caveats Associated With **Vector API**
     
      Firstly, this API is still in the incubation phase. There is, however, a plan to have vector classes declared as primitive classes. 

      As mentioned above, the Vector API has a **hardware dependency** as it relies on **SIMD** instructions. Many of the features may not be available on other platforms and architectures. Moreover, there is always an overhead of maintaining vectorized operations over traditional scalar ones.

      It is also difficult to perform benchmark comparisons of vector operations on generic hardware without knowing the underlying architecture. 

      Currently, It is not a goal to support vector instructions on CPU architectures other than x64 and AArch64.

25. What is a **strongly typed** programming language?
   
    **Strong typing** is a phrase with no widely agreed upon meaning. Most programmers who use this term to mean something other than static typing use it to imply that there is a type discipline that is enforced by the compiler. **Weak typing** implies that the compiler does not enforce a typing discipline, or perhaps that enforcement can easily be subverted.

    In a strongly typed language compiler ensure type correctness, for example, you cannot store the number in String or vice-versa. Java is a strongly typed language, that's why you have different data types e.g. int, float, String, char, boolean etc. You can only store compatible values in respective types.   

    On the other hand, weakly typed language don't enforce type checking at compile time and they tree values based upon context. Python and Perl are two popular example of weakly typed programming language, where you can store a numeric string in number type.

    **Static typing** is where the type is bound to the *variable*. Types are checked at compile time.

    **Dynamic typing** is where the type is bound to the *value*. Types are checked at run time.
