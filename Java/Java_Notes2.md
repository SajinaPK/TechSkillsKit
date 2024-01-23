1. Can **Enum** implement interface in Java?

   Yes, Enum can implement interface in Java. Since enum is a type, similar to class and interface, it can implement interface. This gives a lot of flexibility to use Enum as specialized implementation in some cases.

    ```
    public class Main {
      enum Level {
        LOW,
        MEDIUM,
        HIGH
      }

      public static void main(String[] args) {
        Level myVar = Level.MEDIUM; 
        System.out.println(myVar);
      }
    }
    ```
    ```
    interface week { 
  
      // Defining an abstract method 
      public int day(); 
    } 
  
    // Initializing an enum which 
    // implements the above interface 
    enum Day implements week { 
  
        // Initializing the possible 
        // days 
        Monday, 
        Tuesday, 
        Wednesday, 
        Thursday, 
        Friday, 
        Saturday, 
        Sunday; 
  
        public int day() { 
          return ordinal() + 1; 
      } 
    } 
  
    // Main Class 
    public class Daycount { 
      public static void main(String args[]) { 
        System.out.println("It is day number "  + Day.Wednesday.day() + " of a week."); 
      } 
    } 
    ```

    ```
    interface EnumInterface {
       int calculate(int first, int second);
    }
    enum EnumClassOperator implements EnumInterface { // An Enum implements an interface
       ADD {
          @Override
          public int calculate(int first, int second) {
             return first + second;
          }
       },
       SUBTRACT {
        @Override
        public int calculate(int first, int second) {
           return first - second;
        }
       };
    }
    class Operation {
       private int first, second;
       private EnumClassOperator operator;
       public Operation(int first, int second, EnumClassOperator operator) {
          this.first = first;
          this.second = second;
          this.operator = operator;
       }
       public int calculate() {
          return operator.calculate(first, second);
       }
    }
    // Main Class
    public class EnumTest {
       public static void main (String [] args) {
          Operation add = new Operation(20, 10, EnumClassOperator.ADD);
          Operation subtract = new Operation(20, 10, EnumClassOperator.SUBTRACT);
          System.out.println("Addition: " + add.calculate());
          System.out.println("Subtraction: " + subtract.calculate());
       }
    }
    ```

2. Can **Enum extends class** in Java?

   No, Enum can not extend class in Java. Since all Enum by default extend abstract base class java.lang.Enum, obviously they can not extend another class, because Java doesn't support multiple inheritance for classes. Because of extending java.lang.Enum class, all enum gets methods like ordinal(), values() or valueOf().

3. Java **Singletons Using Enum**
  
   When making singleton classes, consider using an enum. It solves the problems that can crop up with (de)serialization and reflection.

   **Advantages of using Enum as Singleton:**  
   - Enum Singletons are easy to write
     ```
     public enum EasySingleton{
        INSTANCE;
      }
     ```
   - Enum Singletons handled Serialization by themselves
   - Creation of Enum instance is thread-safe

4. What are different Reference types available in Java, e.g. **WeakReference, SoftReference or PhantomReference**? and Why should you use them?

   They are different reference types coming from java.lang.ref package and provided to assist Java **Garbage Collector** in a case of low memory issues. If you wrap an object with WeakReference than it will be eligible for garbage collected if there are no strong reference. They can later be reclaimed by Garbage collector if JVM is running low on memory.

   The `java.util.WeakHashMap` is a special Map implementation, whose keys are the object of **WeakReference**, so if only Map contains the reference of any object and no other, those object can be garbage collected if GC needs memory.

   A **hard (or strong) reference** is the default type of reference, and most of the time, we may not even think about when and how referenced objects are garbage collected. The object can’t be garbage collected if it’s reachable through any strong reference.

   All **soft references** to objects reachable only by soft reference should be cleared out before the OutOfMemoryError exception is thrown.

   **Soft references** can be used to make our code more resilient to errors connected to insufficient memory. For example, we could create a memory-sensitive cache that automatically evicts objects when memory is scarce. We wouldn’t need to **manage the memory manually**, as the garbage collector would do it for us.

   **Weak references** are most often used to create canonicalizing mappings. These are mappings that map only objects that can be reached. A great example is WeakHashMap, which works like normal HashMap, but its keys are weakly referenced, and they are automatically removed when the referent is cleared.

   Using **WeakHashMap**, we can create a **short-living cache** that clears objects that are no longer used by other parts of the code. If we used a normal HashMap, the mere existence of the key in the map would prohibit it from being cleared by the garbage collector.

   Similarly to weak references, **phantom references** don’t prohibit the garbage collector from enqueueing objects for being cleared. The difference is phantom references must be manually polled from the reference queue before they can be finalized. That means we can decide what we want to do before they are cleared. Important use cases for phantom references are **cleanup logic, debugging and memory leak detection**.

5. **Nested classes can be static or non-static** (also called an inner class). How do you decide which to use? Does it matter?

   The key difference between them is that inner classes have full access to the fields and methods of the enclosing class. This can be convenient for event handlers, but comes at a cost: every instance of an inner class retains and requires a reference to its enclosing class.
   
   With this cost in mind, there are many situations where we should prefer static nested classes. When instances of the nested class will **outlive instances of the enclosing class**, the nested class should be static to prevent memory leaks.

   ```
   public class OuterClass {  
      private static int outerStaticField = 10;
      private int outerInstanceField = 20;  
  
      // Static nested class  
      public static class StaticNestedClass {  
         private int nestedField;  
  
         public StaticNestedClass(int nestedField) {  
            this.nestedField = nestedField;  
         }  
      public void display() {  
         // Accessing the static field from the outer class  
         System.out.println("Outer static field: " + outerStaticField);  
         // Accessing the field of the static nested class  
         System.out.println("Nested field: " + nestedField);  
        }  
    }  

    public static void main(String[] args) {  
        // Creating instances of the static nested class  
        StaticNestedClass nestedObject1 = new StaticNestedClass(30);  
        StaticNestedClass nestedObject2 = new StaticNestedClass(40);  
  
        // Calling the display() method of the static nested class  
        nestedObject1.display(); // Output: Outer static field: 10, Nested field: 30  
        nestedObject2.display(); // Output: Outer static field: 10, Nested field: 40  
  
        // Accessing static nested class directly without an instance of the outer class  
        OuterClass.StaticNestedClass DirectAccess = new OuterClass.StaticNestedClass(50);  
        DirectAccess.display(); // Output: Outer static field: 10, Nested field: 50  
    }  
   }  
   ```
   Non-Static (Inner) Nested Class

   ```
   public class OuterClass {
      private int outerInstanceField;  
  
       public OuterClass(int outerInstanceField) {
         this.outerInstanceField = outerInstanceField;  
       }  
  
       // Non-static (inner) nested class
      public class InnerClass {  
         private int innerInstanceField;  
         public InnerClass(int innerInstanceField) {  
            this.innerInstanceField = innerInstanceField;  
         }  
  
        public void display() {  
            // Accessing the instance field from the outer class  
            System.out.println("Outer instance field: " + outerInstanceField);  
            // Accessing the instance field from the inner class  
            System.out.println("Inner instance field: " + innerInstanceField);  
        }  
       }  
  
       public static void main(String[] args) {
         // Create an instance of the outer class  
         OuterClass outerObject = new OuterClass(10);  
  
        // Create an instance of the inner class using the outer class instance  
        InnerClass innerObject = outerObject.new InnerClass(20);  
  
        // The display() method of the inner class is being called  
        innerObject.display();  
       }  
   }  
   ```

6. What occurs when an **object is constructed**?

   Several things happen in a specific order to guarantee the object is constructed properly:
   - **Memory is allocated**. Memory is distributed from heap to hold all instance variables and implementation-specific data of the object and its superclasses
   - Fields are initialized to their default values.
   - The "first line" of the chosen constructor is invoked, unless it's an Object. By first line I mean either explicit call to **super() or this()**, or an implicit call to super().
   - The instance **initializer** is executed and the fields are initialized to their requested values (actually field initialization is usually compiled as an inline part of the instance initializer).
The rest of the constructor code is executed.

7. What is **classloader**?

     ClassLoader - It is a subsystem of JVM which is used to load class files. It is mainly responsible for three activities. Loading, Linking, Initialization
      
      The classloader is a subsystem of JVM that is used to load classes and interfaces.There are many types of classloaders e.g. Bootstrap classloader, Extension classloader, System classloader, Plugin classloader etc.
   - **Bootstrap Classloader**: Loads core java API file rt.jar from folder.
   - **Extension Classloader**: Loads jar files from folder.
   - **System/Application Classloader**: Loads jar files from path specified in the CLASSPATH environment variable.

8. How many types of memory areas are allocated by JVM?

   - **Class(Method) Area**: Class Area stores per-class structures such as the runtime constant pool, field, method data, and the code for methods.
   - **Heap**: It is the runtime data area in which the memory is allocated to the objects
   - **Stack**: Java Stack stores frames. It holds local variables and partial results, and plays a part in method invocation and return. Each thread has a private JVM stack, created at the same time as the thread. A new frame is created each time a method is invoked. A frame is destroyed when its method invocation completes.
   - **Program Counter Register**: PC (program counter) register contains the address of the Java virtual machine instruction currently being executed.
   - **Native Method Stack**: It contains all the native methods used in the application

9. **JIT Compiler**
    
   Just in time compiler or JIT is an integral component of Java Virtual Machine along with Garbage collector, which as name suggest does Just in time compilation. It is capable of compiling Java code directly into machine language, which can greatly improve performance of Java application.
   
   By the way, its not guaranteed that which code will be compiled and when. JIT usually compile hot code in Hotspot JVM once its execution cross certain limit e.g. a method will be converted into machine language if it is called more than 10K times etc.

   Another difference between JIT and JVM is that, JIT is part of JVM. One example of JIT is Oracle's Hotspot JIT which comes with Hotspot JVM. It is called hotpost because its Just in time compiler compiles only hot code into native language, code which execute 90% of time.

   There is threshold setup, if some code executes more than that threshold then it become eligible for just in time compiled. By the way, Hotspot is not the only JVM which contains Just in time compilers, there are others JVM as well e.g. Oracle's original JRockit one.

10. How is a **code point related to a code unit in Unicode**?
   
    A code unit is the number of bits an encoding uses. So UTF-8 would use 8 and UTF-16 would use 16 units. A code point is a character and this is represented by one or more code units depending on the encoding.  
   String.length returns number of code units (UTF-16 values) and *not* number of characters (code points).

11. Is **Empty .java file name** a valid source file name?
   
    Yes, save your java file by .java only, compile it by javac .java and run by java yourclassname.

12. What is a Character set?

    A character is a minimal unit of text that has semantic value.  
    A character set is a collection of characters that might be used by multiple languages. For example, the Latin character set is used by English and most European languages, though the Greek character set is used only by the Greek language.  
    A coded character set is a character set where each character is assigned a unique number.  
    A code point is a value that can be used in a coded character set. A code point is a 32-bit int data type, where the lower 21 bits represent a valid code point value and the upper 11 bits are 0.  
    A Unicode code unit is a 16-bit char value. For example, imagine a String that contains the letters "abc" followed by the Deseret LONG I, which is represented with two char values. That string contains four characters, four code points, but five code units.

    One of the earliest encoding schemes, called ASCII (American Standard Code for Information Exchange) uses a single-byte encoding scheme. This essentially means that each character in ASCII is represented with seven-bit binary numbers. This still leaves one bit free in every byte!

    Let’s define a simple method in Java to display the binary representation for a character under a particular encoding scheme:
      ```
      String convertToBinary(String input, String encoding) throws UnsupportedEncodingException {
         byte[] encoded_input = Charset.forName(encoding)
            .encode(input)
            .array();  
       return IntStream.range(0, encoded_input.length)
        .map(i -> encoded_input[i])
        .mapToObj(e -> Integer.toBinaryString(e ^ 255))
        .map(e -> String.format("%1$" + Byte.SIZE + "s", e).replace(" ", "0"))
        .collect(Collectors.joining(" "));
      }
      ```
13. What is the difference between static (class) method and instance method?

| **Static Methods**                              | **Instance Methods**                                           |
|-------------------------------------------------|----------------------------------------------------------------|
| Can be called without the object of the class.  | Require an object of the class.                                |
| Associated with the class.                      | Associated with the objects.                                   |
| Can only access static attributes of the class. | Can access all the attributes of the class.                    |
| Declared with the static keyword.               | Do not require any keywords.                                   |
| Exists as a single copy for a class.            | Exist as multiple copies depending on the number of instances. |

For example: public static int cube(int n){ return n*n*n;}	For example: public void msg(){...}.

14. How is the difference between **thread and process**?
   
    A process runs in its own address space. No two processes share their address space. Threads will run in the same address space of the process that owns them. Two process runs on different memory space, but all threads share same memory space.
    
    Don't confuse this with stack memory, which is different for the different thread and used to store local data to that thread.
     
    Both processes and threads are independent sequences of execution. The typical difference is that threads (of the same process) run in a shared memory space, while processes run in separate memory spaces.

15. Why Java is **not fully objective oriented** ?
   
    Due to the use of primitives in java, which are not objects.

16. What is a **marker interface** ?
   
    An interface that contains no methods. Eg: Serializable, Cloneable, SingleThreadModel etc. It is used to just mark java classes that support certain capability. An empty interface used to add metadata similar to annotation.

17. What are tag interfaces?
   
    Tag interface is an alternate name for marker interface.
    
18. What is **blank final variable**?
    
    A final variable, not initalized at the time of declaration, is known as blank final variable.

19. Can we intialize blank final variable?
   
    Yes, only in constructor if it is non-static. If it is static blank final variable, it can be initialized only in the static block

20. Why can't **this() and super() both be used together in a constructor**?
   
    Constructor must always be the first statement.
    
   So we can not have two statements as first statement, hence either we can call `super()` or we can call `this()` from the constructor, but not both.
   `this(...)` will call another constructor in the same class whereas `super()` will call a super constructor. If there is no `super()` in a constructor the compiler will add one implicitly. 
   
   Thus if both were allowed you could end up calling the super constructor twice.
