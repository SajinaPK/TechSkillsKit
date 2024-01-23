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

3. 
