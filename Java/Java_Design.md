1. **What is the 5 objects oriented design principle from SOLID?**

    The goal is to improve the reusability of the code and reduce the frequency with which you need to change a class:
    - **S for Single Responsibility Principle**
    - **O for Open closed design principle**
    - **L for Liskov substitution principle**
    - **I for Interface segregation principle**
    - **D for Dependency inversion principle**

    **S** -  A class should only have one responsibility. Furthermore, it should only have one reason to change.

    **O** -  Classes should be open for extension but closed for modification. In doing so, we stop ourselves from modifying existing code and causing potential new bugs. One exception to the rule is when fixing bugs in existing code.
  
    **L** - If class A is a subtype of class B, we should be able to replace B with A without disrupting the behavior of our program. Do not add classes which change the behavior of our program like ex to a class of Car do not add a subtype of ElectricCar which doesn't have turnOnEngine() method/function.
  
    **I** - Larger interfaces should be split into smaller ones. By doing so, we can ensure that implementing classes only need to be concerned about the methods that are of interest to them.
  
    **D** - The principle of dependency inversion refers to the decoupling of software modules. This way, instead of high-level modules depending on low-level modules, both will depend on abstractions.

2. **What is dependency injection?**
   
    Dependency injection is a programming technique that makes a class independent of its dependencies. It achieves that by decoupling the usage of an object from its creation. This helps you to follow SOLID’s dependency inversion and single responsibility principles.

    Dependency injection supports SOLID by decoupling the creation of the usage of an object. That enables you to replace dependencies without changing the class that uses them

    If you want to use this technique, you need classes that fulfill four basic roles. These are:

    1\. The service you want to use.  
    2\. The client that uses the service.  
    3\. An interface that’s used by the client and implemented by the service.  
    4\. The injector which creates a service instance and injects it into the client.  


3. **Which design pattern will you use to shield your code from a third party library which will likely to be replaced by another in couple of months?**
   
    One way to shield your code from third party library is to **code against an interface rather than implementation** and then **use dependency injection** to provide a particular implementation.


4. **What are the types of design patterns in Java?**
    There are four types of design patterns in Java:
    - **Creational** - These design patterns provide a way to create objects while hiding the creation logic, rather than instantiating objects directly using new operator. This gives program more flexibility in deciding which objects need to be created for a given use case.  
    - **Structural** - These design patterns concern class and object composition. Concept of inheritance is used to compose interfaces and define ways to compose objects to obtain new functionalities.  
    - **Behavioral** - These design patterns are specifically concerned with communication between objects.  
    - **J2EE** - These design patterns are specifically concerned with the presentation tier. These patterns are identified by Sun Java Center.  
