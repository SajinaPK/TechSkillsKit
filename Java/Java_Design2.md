1. **Behavioural Design Patterns in Java**
   
  - **Chain Of Responsibility Method** - Avoid coupling the sender of request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.
  - **Command Method** - Also known as **Action, Transaction.** It encapsulate a request tan object, parameterize clients with different requests, queue or log requests and support undoable operations.
  - **Interpreter Method** - Provides a way to evaluate language grammar or expression. This pattern is used in SQL parsing, symbol processing engine etc.
  - **Mediator Method** - Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it vary from their interaction independently.
  - **Memento Method**
  - **Observer method**
  - **State Method**
  - **Strategy Method**
  - **Template Method**
  - **Visitor Method**
  - **Null Object Method**


2. **Chain Of Responsibility Method - Behavioural Design Pattern**

    It creates a chain of receiver objects for a request. This pattern decouples sender and receiver of a request based on type of request.
    In this pattern, normally each receiver contains reference to another receiver. If one object cannot handle the request then it passes the same to the next receiver and so on.

    **Components**

    1\. **Handler** : This can be an interface which will primarily receive the request and dispatches the request to a chain of handlers. It has reference to the only first handler in the chain and does not know anything about the rest of the handlers.
   
    2\. **Concrete handlers** : These are actual handlers of the request chained in some sequential order.
   
    3\. **Client** : Originator of request and this will access the handler to handle it.

    **When to use Chain of Responsibility Method**

    - When you want to decouple a request’s sender and receiver
    - Multiple objects, determined at runtime, are candidates to handle a request
    - When you don’t want to specify handlers explicitly in your code
    - When you want to issue a request to one of several objects without specifying the receiver explicitly.

      ```
      // Each logger checks the level of message to its level and print accordingly otherwise does not print and pass the message to its next logger.
	    public abstract class AbstractLogger {
          public static int INFO = 1;
          public static int DEBUG = 2;
          public static int ERROR = 3;
          protected int level;

          //next element in chain or responsibility
          protected AbstractLogger nextLogger;

          public void setNextLogger(AbstractLogger nextLogger){
           this.nextLogger = nextLogger;
          }

          public void logMessage(int level, String message){
           if(this.level <= level){
             write(message);
           }
           if(nextLogger !=null){
             nextLogger.logMessage(level, message);
           }
          }

          abstract protected void write(String message);
	      }

        // Create concrete classes extending the logger.
        public class ConsoleLogger extends AbstractLogger {
           public ConsoleLogger(int level){
           this.level = level;
           }
           @Override
           protected void write(String message) {		
              System.out.println("Standard Console::Logger: " + message);
           }
        }

        public class ErrorLogger extends AbstractLogger {
         public ErrorLogger(int level){
          this.level = level;
         }
         @Override
         protected void write(String message) {		
            System.out.println("Error Console::Logger: " + message);
         }
        }

        public class FileLogger extends AbstractLogger {
          public FileLogger(int level){
            this.level = level;
         }
         @Override
         protected void write(String message) {		
            System.out.println("File::Logger: " + message);
         }
        }

        // Create different types of loggers. Assign them error levels and set next logger in each logger. Next logger in each logger represents the part of the chain.

        public class ChainPatternDemo {
          private static AbstractLogger getChainOfLoggers(){

          AbstractLogger errorLogger = new ErrorLogger(AbstractLogger.ERROR);
          AbstractLogger fileLogger = new FileLogger(AbstractLogger.DEBUG);
          AbstractLogger consoleLogger = new ConsoleLogger(AbstractLogger.INFO);

          errorLogger.setNextLogger(fileLogger);
          fileLogger.setNextLogger(consoleLogger);

          return errorLogger;	
         }

         public static void main(String[] args) {
            AbstractLogger loggerChain = getChainOfLoggers();

            loggerChain.logMessage(AbstractLogger.INFO, "This is an information.");
            loggerChain.logMessage(AbstractLogger.DEBUG, "This is an debug level information.");
            loggerChain.logMessage(AbstractLogger.ERROR, "This is an error information.");
           }
        }
      ```
      ```
      Standard Console::Logger: This is an information.
      File::Logger: This is an debug level information.
      Standard Console::Logger: This is an debug level information.
      Error Console::Logger: This is an error information.
      File::Logger: This is an error information.
      Standard Console::Logger: This is an error information.
      ```
