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
  
5. **Creational Design Patterns in Java**

      - **Factory Method** – Creates objects of several related classes without specifying the exact object to be created
      - **Abstract Factory** – Creates families of related dependent objects
      - **Builder** – Constructs complex objects using step-by-step approach
      - **Singleton** – Ensures that at most only one instance of an object exists throughout application
      - **Prototype** - Lets you copy existing objects without making your code dependent on their classes. The concept is to copy an existing object rather than creating a new instance from scratch

7. **Factory Method pattern - Creational Design Patterns**

    Used to create objects without specifying the exact class of object that will be created. This pattern is useful when you need to decouple the creation of an object from its implementation.
   
   The idea is to create a factory class with a single responsibility to create objects, hiding the details of class modules from the user.
    ```
    class ThreeWheeler extends Vehicle {
    public void printVehicleInfo()
    {
        System.out.println("I am three wheeler");
    }
    }
 
    class FourWheeler extends Vehicle {
    public void printVehicleInfo()
    {
        System.out.println("I am four wheeler");
    }
    }

    class VehicleFactory {
 
    Vehicle build(VehicleType vehicleType)
    {
        if (VehicleType.VT_TwoWheeler.compareTo(vehicleType)
            == 0) {
            return new TwoWheeler();
        }
        else if (VehicleType.VT_ThreeWheeler.compareTo(
                     vehicleType)
                 == 0) {
            return new ThreeWheeler();
        }
        else if (VehicleType.VT_FourWheeler.compareTo(
                     vehicleType)
                 == 0) {
            return new FourWheeler();
        }
        return null;
    }
    }
    ```
    Other examples of the Factory Method:

    - In a **Drawing** system, depending on the user’s input, different pictures like squares, rectangles, the circle can be drawn. 
    - On the **travel tickets** site, we can book train tickets as well as bus tickets and flight tickets. In this case, the user can give his travel type as ‘bus’, ‘train’, or ‘flight’.
  
7. **Abstract Factory Method - Creational Design Patterns**

    Abstract Factory pattern is almost similar to Factory Pattern and is considered as another layer of abstraction over factory pattern. Abstract Factory patterns work around a super-factory which creates other factories.

      **Difference**

    - The main difference between a “factory method” and an “abstract factory” is that the factory method is a single method, and an abstract factory is an object. 
    - The factory method is just a method, it can be overridden in a subclass, whereas the abstract factory is an object that has multiple factory methods on it.
    - The Factory Method pattern uses inheritance and relies on a subclass to handle the desired object instantiation.

     **Disadvantages**

    - Difficult to support new kinds of products: Extending abstract factories to produce new kinds of Products isn’t easy. That’s because the AbstractFactory interface fixes the set of products that can be created. Supporting new kinds of products requires extending the factory interface, which involves changing the AbstractFactory class and all of its subclasses.

    **When to use**
    - When the system must be independent in terms of how its objects are created, composed, and represented.
    - This constraint must be enforced when a family of related objects needs to be used together.
    - When you want to provide an object library that does not show implementations but only exposes interfaces.
    - When the system has to be configured with one of several families of objects.

    **Examples**
    - A family of related products, say: Chair + Sofa + CoffeeTable.  
    Several variants of this family. For example, products Chair + Sofa + CoffeeTable are available in these variants: Modern, Victorian, ArtDeco.  
    You need a way to create individual furniture objects so that they match other objects of the same family.

    - We need car factories in each location like IndiaCarFactory, USACarFactory, and DefaultCarFactory. Now, our application should be smart enough to identify the location where it is being used, so we should be able to use the appropriate car factory without even knowing which car factory implementation will be used internally.
  
8. **Builder Method - Creational Design Patterns**

    Builder pattern aims to “Separate the construction of a complex object from its representation so that the same construction process can create different representations.” It is used to construct a complex object step by step and the final step will return the object. The process of constructing an object should be generic so that it can be used to create different representations of the same object.

    **Components**
   
    1\. **Product** – The product class defines the type of the complex object that is to be generated by the builder pattern.
   
    2\. **Builder** – This abstract base class defines all of the steps that must be taken in order to correctly create a product. Each step is generally abstract as the actual functionality of the builder is carried out in the concrete subclasses.
   
    3\. **ConcreteBuilder** – There may be any number of concrete builder classes inheriting from Builder. These classes contain the functionality to create a particular complex product.
   
    4\. **Director** – The director-class controls the algorithm that generates the final product object. A director object is instantiated and its Construct method is called. The method includes a parameter to capture the specific concrete builder object that is to be used to generate the product. 

    ```
    interface HousePlan 
    { 
    public void setBasement(String basement); 
    public void setStructure(String structure); 
    public void setRoof(String roof); 
    public void setInterior(String interior); 
    } 
  
    class House implements HousePlan { 
    private String basement; 
    private String structure; 
    private String roof; 
    private String interior; 
  
    public void setBasement(String basement)  { 
        this.basement = basement; 
    } 
  
    public void setStructure(String structure)  { 
        this.structure = structure; 
    } 
  
    public void setRoof(String roof)  { 
        this.roof = roof; 
    } 
  
    public void setInterior(String interior)  { 
        this.interior = interior; 
    } 
    } 
  
    interface HouseBuilder 
    { 
    public void buildBasement(); 
    public void buildStructure(); 
    public void buildRoof(); 
    public void buildInterior(); 
    public House getHouse(); 
    }
    
    class IglooHouseBuilder implements HouseBuilder { ... }
    class TipiHouseBuilder implements HouseBuilder { ... }

    class CivilEngineer  { 
    private HouseBuilder houseBuilder; 
    public CivilEngineer(HouseBuilder houseBuilder) { 
        this.houseBuilder = houseBuilder; 
    } 
  
    public House getHouse() { 
        return this.houseBuilder.getHouse(); 
    } 
  
    public void constructHouse() { 
        this.houseBuilder.buildBasement(); 
        this.houseBuilder.buildStructure(); 
        this.houseBuilder.buildRoof(); 
        this.houseBuilder.buildInterior(); 
    } 
    } 

    class Builder { 
    public static void main(String[] args) { 
        HouseBuilder iglooBuilder = new IglooHouseBuilder(); 
        CivilEngineer engineer = new CivilEngineer(iglooBuilder); 
        engineer.constructHouse(); 
        House house = engineer.getHouse(); 
        System.out.println("Builder constructed: "+ house); 
    } 
    }
    ```
9. **Singleton Method - Creational Design Patterns**

    A Singleton class provides one unique global access point to the object so that each subsequent call to the access point returns only that particular object.
    
    **When to Use Singleton Design Pattern**

    - For resources that are expensive to create (like database connection objects)
    - It’s good practice to keep all loggers as Singletons which increases performance
    - Classes which provide access to configuration settings for the application
    - Classes that contain resources that are accessed in shared mode
    - ex: logging, driver objects, caching, and thread pool, database connections.

    **Singleton Pattern Example**
   ```
   public class Singleton  {    
    private Singleton() {}
    
    private static class SingletonHolder {    
        public static final Singleton instance = new Singleton();
    }

    public static Singleton getInstance() {    
        return SingletonHolder.instance;    
    }
    }
    ```
   - It employs a **static member** within the class. This static member ensures that memory is allocated only once, preserving the single instance of the Singleton class.
   - Incorporates a **private constructor**, which serves as a barricade against external attempts to create instances of the Singleton class.
   - The **static factory method** acts as a gateway, providing a global point of access to the Singleton object. When someone requests an instance, this method either creates a new instance (if none exists) or returns the existing instance to the caller.
  
     In the above code example, we’ve created a **static inner class** that holds the instance of the Singleton class. It creates the instance only when someone calls the getInstance() method and not when the outer class is loaded.

    This is a widely used approach for a Singleton class as **it doesn’t require synchronization, is thread safe, enforces lazy initialization and has comparatively less boilerplate**.

10. **Prototype Method - Creational Design Patterns**

    The concept is to copy an existing object rather than creating a new instance from scratch, something that may include costly operations. The existing object acts as a prototype and contains the state of the object. The newly copied object may change same properties only if required. 

    One of the best available ways to create an object from existing objects is the **clone() method**. Clone is the simplest approach to implement a prototype pattern.

    **Components**

    1\. **Prototype** : This is the prototype of an actual object.
    
    2\. **Prototype registry** : This is used as a registry service to have all prototypes accessible using simple string parameters.
    
    3\. **Client** : Client will be responsible for using registry service to access prototype instances.

    **When to Use**
    - When a system should be independent of how its products are created, composed, and represented and 
    - When the classes to instantiate are specified at run-time. 

    ```
    abstract class Color implements Cloneable {   
    protected String colorName;     
    abstract void addColor();
      
    public Object clone() {
        Object clone = null;
        try {
            clone = super.clone();
        } 
        catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return clone;
    }
    }

    class blueColor extends Color    {
    public blueColor() {
        this.colorName = "blue";
    }
    @Override
    void addColor() {
        System.out.println("Blue color added");
    }    
    }

    class blackColor extends Color{
    public blackColor() {
        this.colorName = "black";
    } 
    @Override
    void addColor() {
        System.out.println("Black color added");
    }
    }

    class ColorStore {
      private static Map<String, Color> colorMap = new HashMap<String, Color>();     
        static {
            colorMap.put("blue", new blueColor());
            colorMap.put("black", new blackColor());
        }
      
        public static Color getColor(String colorName) {
            return (Color) colorMap.get(colorName).clone();
        }
    }

    // Driver class
    class Prototype {
    public static void main (String[] args) {
        ColorStore.getColor("blue").addColor();
        ColorStore.getColor("black").addColor();
        ColorStore.getColor("black").addColor();
        ColorStore.getColor("blue").addColor();
    }
    }
    ```

11. **Structural Design Patterns in Java**
    - **Adapter Method** - Also known as **wrapper**. It convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.
    - **Bridge Method** - Also known as **Handle/Body**. Decouple an abstraction from its implementation so that the two can vary independently.
    - **Composite Method** - Compose objects into **tree structures to represent part-whole hierarchies**. Composite lets clients treat individual objects and compositions of objects uniformly.
    - **Decorator Method** - Attach with additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.
    - **Facade Method** - Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.
    - **Proxy Method** - Also known as **Surrogate**, it provide a surrogate or placeholder for another object to control access to it.
    - **Flyweight Method** - Used to support large numbers of fine-grained objects efficiently.

12. **Adapter Design Patterns - Structural Design Pattern**

    Allows the interface of an existing class to be used as another interface. It acts as a bridge between two incompatible interfaces, making them work together.
    
    **Components**

    1\. **Target Interface** - It’s the common interface that the client code interacts with.

    2\. **Adaptee** -  It’s the class or system that the client code cannot directly use due to interface mismatches.

    3\. **Adapter** - It acts as a bridge, adapting the interface of the adaptee to match the target interface.

    4\. **Client** - It’s the code that benefits from the integration of the adaptee into the system through the adapter.
    ```
    // Target Interface
    class Printer {
    public:
        virtual void print() = 0;
    };
 
    // Adaptee
    class LegacyPrinter {
    public:
        void printDocument() {
            std::cout << "Legacy Printer is printing a document." << std::endl;
        }
    };
 
    // Adapter
    class PrinterAdapter : public Printer {
    private:
        LegacyPrinter legacyPrinter;
 
    public:
        void print() override {
            legacyPrinter.printDocument();
        }
    };
 
    // Client Code
    void clientCode(Printer& printer) {
        printer.print();
    }
 
    int main() {
        // Using the Adapter
        PrinterAdapter adapter;
        clientCode(adapter);
        return 0;
    }
    ```
    
    **When to use Adapter Method**

    - You want to use an existing class, and its interface does not match the one you need.
    - You want to create a reusable class that cooperates with unrelated orunforeseen classes, that is, classes that don’t necessarily have compatible interfaces.
    - (object adapter only) you need to use several existing subclasses, but it’s unpractical to adapt their interface by subclassing every one. An object adapter can adapt the interface of its parent class.
    - You want to share an implementation among multiple objects(perhaps using reference counting), and this fact should be hidden from the client.

13. **Bridge Design Patterns - Structural Design Pattern**

    The Bridge design pattern allows you to separate the abstraction from the implementation
    
    **Components**
    
    1\. **Abstraction** – core of the bridge design pattern and defines the crux. Contains a reference to the implementer.

    2\. **Refined Abstraction** – Extends the abstraction takes the finer detail one level below. Hides the finer elements from implementers.

    3\. **Implementer** – It defines the interface for implementation classes. This interface does not need to correspond directly to the abstraction interface and can be very different. 

    4\. **Concrete Implementation** – Implements the above implementer by providing the concrete implementation.
    ```
    // abstraction in bridge pattern
    abstract class Vehicle {
        protected Workshop workShop1;
        protected Workshop workShop2;
        protected Vehicle(Workshop workShop1, Workshop workShop2) {
            this.workShop1 = workShop1;
            this.workShop2 = workShop2;
        }
 
        abstract public void manufacture();
    }
 
    // Refine abstraction 1 in bridge pattern
    class Car extends Vehicle {
        public Car(Workshop workShop1, Workshop workShop2) {
        super(workShop1, workShop2);
        }
 
        @Override
        public void manufacture() {
            System.out.print("Car ");
            workShop1.work();
            workShop2.work();
        }
    }
 
    // Refine abstraction 2 in bridge pattern
    class Bike extends Vehicle {
        public Bike(Workshop workShop1, Workshop workShop2) {
            super(workShop1, workShop2);
        }
 
        @Override
        public void manufacture() {
            System.out.print("Bike ");
            workShop1.work();
            workShop2.work();
        }
    }
 
    // Implementer for bridge pattern
    interface Workshop {
        abstract public void work();
    }
 
    // Concrete implementation 1 for bridge pattern
    class Produce implements Workshop {
        @Override
        public void work() {
            System.out.print("Produced");
        }
    }
 
    // Concrete implementation 2 for bridge pattern
    class Assemble implements Workshop {
        @Override
        public void work() {
            System.out.print(" And");
            System.out.println(" Assembled.");
        }
    }
 
    // Demonstration of bridge design pattern
    class BridgePattern {
        public static void main(String[] args) {
            Vehicle vehicle1 = new Car(new Produce(), new Assemble());
            vehicle1.manufacture();
            Vehicle vehicle2 = new Bike(new Produce(), new Assemble());
            vehicle2.manufacture();
        }
    }
    ```
    **When to use Bridge Method**

    - You want to avoid a permanent binding between an abstraction and its implementation. This might be the case,for example,when the implementation must be selected or switched at run-time.
    - Both the abstractions and their implementations should be extensible by subclassing. In this case, the Bridge pattern lets you combine the different abstractions and implementations and extend them independently.
    - Changes in the implementation of an abstraction should have no impact on clients; that is, their code should not have to be recompiled.

14. **Composite Design Patterns - Structural Design Pattern**

    Allows you to compose objects into tree structures to represent part-whole hierarchies. The main idea behind the Composite Pattern is to build a tree structure of objects, where individual objects and composite objects share a common interface. The parts for example are individual shapes (like circles, rectangles) and the wholes are the complex shapes (like a smiley face composed of circles and rectangles).

    **Use Cases of Composite Pattern**

    - **Graphics and GUI Libraries**: Building complex graphical structures like shapes and groups.
    - **File Systems**: Representing files, directories, and their hierarchical relationships.
    - **Organization Structures**: Modeling hierarchical organizational structures like departments, teams and employees.

    **Components**

    1\. **Component**: The Component is the common interface for all objects in the composition. It defines the methods that are common to both leaf and composite objects.
    2\. **Leaf**: The Leaf is the individual object that does not have any children. It implements the component interface and provides the specific functionality for individual objects.
    3\. **Composite**: The Composite is the container object that can hold Leaf objects as well as the other Composite objects. It implements the Component interface and provides methods for adding, removing and accessing children.
    4\. **Client**: The Client is responsible for using the Component interface to work with objects in the composition. It treats both Leaf and Composite objects uniformly.
    ```
    // Component
    class FileSystemComponent { 
    public: 
        virtual void display() const = 0; 
    }; 

    // Leaf
    class File : public FileSystemComponent { 
    public: 
        File(const std::string& name, int size) 
            : name(name) 
            , size(size) { 
        } 
  
        void display() const override { 
            std::cout << "File: " << name << " (" << size 
                  << " bytes)" << std::endl; 
        } 
  
    private: 
        std::string name; 
        int size; 
    }; 

    // Composite
    class Directory : public FileSystemComponent { 
    public: 
        Directory(const std::string& name) 
            : name(name) { 
        } 
  
        void display() const override { 
            std::cout << "Directory: " << name << std::endl; 
            for (const auto& component : components) { 
                component->display(); 
            } 
        } 
  
        void addComponent(FileSystemComponent* component) { 
            components.push_back(component); 
        } 
  
    private: 
        std::string name; 
        std::vector<FileSystemComponent*> components; 
    }; 

    // Client code
    int main() 
    { 
        // Create leaf objects (files) 
        FileSystemComponent* file1 = new File("document.txt", 1024); 
        FileSystemComponent* file2 = new File("image.jpg", 2048); 
  
        // Create a composite object (directory) 
        Directory* directory = new Directory("My Documents"); 
  
        // Add leaf objects to the directory 
        directory->addComponent(file1); 
        directory->addComponent(file2); 
  
        // Display the directory (including its contents) 
        directory->display(); 
  
        return 0; 
    }
    ```
  
    **When to use Composite Method**

    - You want to represent part-whole hierarchies of objects.
    - You want clients to be able to ignore the difference between compositions of objects and individual objects.Clients will treat all objectsin the composite structure uniformly.

15. **Decorator Design Patterns - Structural Design Pattern**

    Decorator pattern allows a user to add new functionality to an existing object without altering its structure.

    ```
    // Create an interface.	
    public interface Shape {
       void draw();
    }

    // Create concrete classes implementing the same interface.
    public class Rectangle implements Shape {
       @Override
       public void draw() {
          System.out.println("Shape: Rectangle");
       }
    }
    // Create concrete classes implementing the same interface.
    public class Circle implements Shape {
       @Override
       public void draw() {
          System.out.println("Shape: Circle");
       }
    }

    // Create abstract decorator class implementing the Shape interface.
    public abstract class ShapeDecorator implements Shape {
       protected Shape decoratedShape;

       public ShapeDecorator(Shape decoratedShape){
          this.decoratedShape = decoratedShape;
       }

       public void draw(){
          decoratedShape.draw();
       }	
    }

    // Create concrete decorator class extending the ShapeDecorator class.
    public class RedShapeDecorator extends ShapeDecorator {

       public RedShapeDecorator(Shape decoratedShape) {
          super(decoratedShape);		
       }

       @Override
       public void draw() {
          decoratedShape.draw();	       
          setRedBorder(decoratedShape);
       }

       private void setRedBorder(Shape decoratedShape){
          System.out.println("Border Color: Red");
       }
    }

    // Client code
    public class DecoratorPatternDemo {
       public static void main(String[] args) {

          Shape circle = new Circle();
          Shape redCircle = new RedShapeDecorator(new Circle());

          Shape redRectangle = new RedShapeDecorator(new Rectangle());
          System.out.println("Circle with normal border");
          circle.draw();

          System.out.println("\nCircle of red border");
          redCircle.draw();

          System.out.println("\nRectangle of red border");
          redRectangle.draw();
       }
    }
    ```
    **When to use Decorator Method**

    - To add responsibilities to individual objects dynamically and transparently, that is, without affecting other objects.
    - For responsibilities that can be withdrawn.
    - When extension by subclassing is impractical. Sometimes a large number of independent extensions are possible and would produce an explosion of subclasses to support every combination. Or a class definition maybe hidden or otherwise unavailable for subclassing.

16. **Facade Design Patterns - Structural Design Pattern**

    Facade Method Design Pattern provides a unified interface to a set of interfaces in a subsystem. Facade defines a high-level interface that makes the subsystem easier to use. Imagine a building, the facade is the outer wall that people see, but behind it is a complex network of wires, pipes, and other systems that make the building function.
It hides the complexity of the underlying system and provides a simple interface that clients can use to interact with the system

    - A Facade to decouple the subsystem from clients and other subsystems, thereby promoting subsystem independence and portability.
    - Facade define an entry point to each subsystem level. If subsystem are dependent, then you can simplify the dependencies between them by making them communicate with each other solely through their facades.

    **Components**

    1\. **Facade (Compiler)** - Facade knows which subsystem classes are responsible for a request. It delegate client requests to appropriate subsystem objects.
    
    2\. **Subsystem classes** (Scanner, Parser, ProgramNode, etc.) - It implement subsystem functionality. It handle work assigned by the Facade object. It have no knowledge of the facade; that is, they keep no references to it.

    Facade Method Design Pattern collaborate in different way

    - Client communicate with the subsystem by sending requests to Facade, which forwards them to the appropriate subsystem objects.
    - The Facade may have to do work of its own to translate it inheritance to subsystem interface.
    - Clients that use the Facade don’t have to access its subsystem objects directly.


    ```
    //Hotel-Keeper is Facade and respective Restaurants is system.
    public interface Hotel {
        public Menus getMenus();
    }

    public class NonVegRestaurant implements Hotel { 
        public Menus getMenus() {
            NonVegMenu nv = new NonVegMenu();
            return nv;
        }    
    }

    public class VegRestaurant implements Hotel {
        public Menus getMenus(){
            VegMenu v = new VegMenu();
            return v;
        }
    }

    public class VegNonBothRestaurant implements Hotel {
        public Menus getMenus() {
            Both b = new Both();
            return b;
        }
    }

    // Facade
    public interface HotelKeeper {
      public VegMenu getVegMenu();
      public NonVegMenu getNonVegMenu();
      public Both getVegNonMenu(); 
    }
    public class HotelKeeperImplementation implements HotelKeeper {
        public VegMenu getVegMenu() {
            VegRestaurant v = new VegRestaurant();
            VegMenu vegMenu = (VegMenu)v.getMenus();
            return vegMenu;
        }
 
        public NonVegMenu getNonVegMenu() {
            NonVegRestaurant v = new NonVegRestaurant();
            NonVegMenu NonvegMenu = (NonVegMenu)v.getMenus();
            return NonvegMenu;
        }
 
        public Both getVegNonMenu() {
            VegNonBothRestaurant v = new VegNonBothRestaurant();
            Both bothMenu = (Both)v.getMenus();
            return bothMenu;
        }
    }

    public class Client {
        public static void main (String[] args) {
            HotelKeeper keeper = new HotelKeeperImplementation();
         
            VegMenu v = keeper.getVegMenu();
            NonVegMenu nv = keeper.getNonVegMenu();
            Both = keeper.getVegNonMenu();
        }
    }
    ```
    **When to use Facade Method**

    - You want to provide a simple interface to a complex subsystem.
    - There are many dependencies between clients and the implementation classes of an abstraction.Introduce a facade to decouple the subsystem from clients and other subsystems, thereby promoting subsystem independence and portability.
    - You want to layer your subsystems. 

17. **Proxy Design Patterns - Structural Design Pattern**

    Controls and manage access to the object they are protecting. Proxy means ‘in place of’, representing’ or ‘in place of’ or ‘on behalf of’ are literal meanings of proxy and that directly explains Proxy Design Pattern. They are closely related in structure, but not purpose, to Adapters and Decorators.

    **Types of proxies**

    - **Remote proxy** - They are responsible for representing the object located remotely. Talking to the real object might involve marshalling and unmarshalling of data and talking to the remote object.

    - **Virtual proxy** - These proxies will provide some default and instant results if the real object is supposed to take some time to produce results.

    - **Protection proxy** - If an application does not have access to some resource then such proxies will talk to the objects in applications that have access to that resource and then get the result back.

    - **Smart Proxy**- Provides additional layer of security by interposing specific actions when the object is accessed. An example can be to check if the real object is locked before it is accessed to ensure that no other object can change it.

    ```
    public interface Internet { 
        public void connectTo(String serverhost) throws Exception; 
    } 

    public class RealInternet implements Internet  { 
        @Override
        public void connectTo(String serverhost) { 
            System.out.println("Connecting to "+ serverhost); 
        } 
    } 

    public class ProxyInternet implements Internet { 
        private Internet internet = new RealInternet(); 
        private static List<String> bannedSites; 
      
        static { 
            bannedSites = new ArrayList<String>(); 
            bannedSites.add("abc.com"); 
            bannedSites.add("def.com"); 
            bannedSites.add("ijk.com"); 
            bannedSites.add("lnm.com"); 
        } 
      
        @Override
        public void connectTo(String serverhost) throws Exception { 
            if(bannedSites.contains(serverhost.toLowerCase())) { 
                throw new Exception("Access Denied"); 
            }    
            internet.connectTo(serverhost); 
        } 
    } 

    public class Client { 
        public static void main (String[] args) { 
            Internet internet = new ProxyInternet(); 
            try { 
                internet.connectTo("geeksforgeeks.org"); 
                internet.connectTo("abc.com"); 
            } 
            catch (Exception e) { 
                System.out.println(e.getMessage()); 
            } 
        } 
    }
    ```
    **When to use Proxy Method**

    Proxy method is applicable whenever there is a need for a more versatile or sophisticated reference to an object than a simple pointer. Here are several common situations in which the Proxy pattern is applicable:

    - A remote proxy provides a local representative for an object in a different address space.
    - A virtual proxy creates expensive objects on demand.
    - A protection proxy controls access to the original object. Protection proxies are useful when objects should have different access rights
    - A smart reference is a replacement for a bare pointer that performs additional actions when an object is accessed.

18. **Flyweight Design Patterns - Structural Design Pattern**

    This pattern provides ways to decrease object count thus improving application required objects structure. Flyweight pattern is used when we need to create a large number of similar objects (say 105). One important feature of flyweight objects is that they are immutable. This means that they cannot be modified once they have been constructed.

    In Flyweight pattern we use a **HashMap** that stores reference to the object which have already been created, every object is associated with a key. Now when a client wants to create an object, he simply has to pass a key associated with it and if the object has already been created we simply get the reference to that object else it creates a new object and then returns it reference to the client.

    **When to use Flyweight Method**

    The Flyweight pattern’s effectiveness depends heavily on how and where it’s used. Apply the Flyweight pattern when all of the following are:
    - An application uses a large number of objects.
    - Storage costs are high because of the sheer quantity of objects.
    - Most object state can be made extrinsic.
    - Many groups of objects may be replaced by relatively few shared objects once extrinsic state is removed.
    - The application doesn’t depend on object identity. Since flyweight objects may be shared, identity tests will return true for conceptually distinct objects.
