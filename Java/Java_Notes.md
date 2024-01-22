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

8. Is String a datatype in Java?  
   The interviewer wanted an explanation which stated that String is not a primitive data type in Java; it is one of the most extensively used objects in Java, which is an instance of String class.

9. String class is defined under which package in Java?  
   The answer to this Java question is java.lang package, and this will test the very basics of core Java knowledge.

10. For-each loop in Java
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

12. 
  
