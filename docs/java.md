![Java](java.png)

# INTRODUCTION TO JAVA

## What is Java ? 
•	Java is an object-oriented programming language developed by Sun Microsystems, and it was released in 1995.

•	James Gosling initially developed Java in Sun Microsystems (which was later merged with Oracle Corporation).

•	Java is a set of features of C and C++. It has obtained its format from C, and OOP features from C++.

•	Java programs are platform independent which means they can be run on any operating system with any processor as long as the Java interpreter is available on that system.

•	Java code that runs on one platform does not need to be recompiled to run on another platform; it's called write once, run any where(WORA).

•	Java Virtual Machine (JVM) executes Java code, but it has been written in platform-specific languages such as C/C++ /ASM, etc. JVM is not written in Java and hence cannot be platform independent, and Java interpreter is a part of JVM.

## History of Java :
The history of Java is very interesting. Java was originally designed for interactive television, but it was too advanced technology for the digital cable television industry at the time. The history of Java starts with the Green Team. Java team members (also known as Green Team), initiated this project to develop a language for digital devices such as set-top boxes, televisions, etc. However, it was suited for internet programming. Later, Java technology was incorporated by Netscape.

The principles for creating Java programming were "Simple, Robust, Portable, Platform-independent, Secured, High Performance, Multithreaded, Architecture Neutral, Object-Oriented, Interpreted, and Dynamic". Java was developed by James Gosling, who is known as the father of Java, in 1995. James Gosling and his team members started the project in the early '90s.

<p align="center">
  <img src="images/gosling.jpg"/>
</p>

James Gosling - founder of java
Currently, Java is used in internet programming, mobile devices, games, e-business solutions, etc. There are given significant points that describe the history of Java.


## Where is java being  used :
Earlier Java was only used to design and program small computing devices, but it was later adopted as one of the platform-independent programming languages, and now according to Sun, 3 billion devices run Java.

•	Java is one of the most important programming languages in today's IT industries.

•	JSP - In Java, JSP (Java Server Pages) is used to create dynamic web pages, such as in PHP and ASP.

•	Applets - Applets are another type of Java programs that are implemented on Internet browsers and are always run as part of a web document.

•	J2EE - Java 2 Enterprise Edition is a platform-independent environment that is a set of different protocols and APIs and is used by various organizations to transfer data between each other.

•	JavaBeans - This is a set of reusable software components that can be easily used to create new and advanced applications.

•	Mobile - In addition to the above technology, Java is widely used in mobile devices nowadays, many types of games and applications are being made in Java.

## Types of java applications :
1.	Web Application - Java is used to create server-side web applications. Currently, Servlet, JSP, Struts, JSF, etc. technologies are used.

2.	Standalone Application - It is also known as the desktop application or window-based application. An application that we need to install on every machine or server such as media player, antivirus, etc. AWT and Swing are used in java for creating standalone applications.

3.	Enterprise Application - An application that is distributed in nature, such as banking applications, etc. It has the advantage of high-level security, load balancing, and clustering. In Java, EJB is used for creating enterprise applications.

4.	Mobile Application - Java is used to create application software for mobile devices. Currently, Java ME is used for building applications for small devices, and also Java is a programming language for Google Android application development.

## Features of java : 

•	Object-Oriented - Java supports the features of object-oriented programming. Its object model is simple and easy to expand.

•	Platform independent - C and C++ are platform dependency languages hence the application programs written in one Operating system cannot run in any other Operating system, but in platform independence language like Java application programs written in one Operating system can able to run on any Operating system.

•	Simple - Java has included many features of C / C ++, which makes it easy to understand.

•	Secure - Java provides a wide range of protection from viruses and malicious programs.  It ensures that there will be no damage and no security will be broken.

•	Portable - Java provides us with the concept of portability. Running the same program with Java on different platforms is possible.

•	Robust - During the development of the program, it helps us to find possible mistakes as soon as possible.

•	Multi-threaded - The multithreading programming feature in Java allows you to write a program that performs several different tasks simultaneously.

•	Distributed - Java is designed for distributed Internet environments as it manages the TCP/IP protocol.


# BASIC CONCEPTS OF OBJECT-ORIENTED PROGRAMMING 

## Objects :

   Objects are the basic runtime entities in an object oriented system. They may represent a person, a place, a bank account, a table of data or any item that the program has to handle.

## Class : 
   Object contains data, and code to manipulate that data. The entire set of data and code of an object can be made a user-defined data type with the help of a class.

 ## Data Encapsulation :
 
   The wrapping up of data and functions into a single unit is known as encapsulation. The data is not accessible to the outside world, only those function which are wrapped in the can access it. These functions provide the interface between the object’s data and the program. This insulation of the data from direct access by the program is called data hiding or information hiding.

## Data Abstraction :

   Abstraction refers to the act of representing essential features without including the background details or explanations. Since classes use the concept of data abstraction, they are known as Abstract Data Types (ADT).

## Inheritance :

   Inheritance is the process by which objects of one class acquire the properties of objects of another class. In OOP, the concept of inheritance provides the idea of reusability. This means we can add additional features to an existing class without modifying it.

## Polymorphism :

   Polymorphism, a Greek term means to ability to take more than one form. An operation may exhibits different behaviors in different instances. The behavior depends upon the type of data used in the operation.
     For example consider the operation of addition for two numbers; the operation will generate a sum. If the operands are string then the operation would produce a third string by concatenation.The process of making an operator to exhibit different behavior in different instances is known operator overloading.


# ABSTRACT CLASS AND INTERFACES 

## Abstract Class :

A class that is declared using “abstract” keyword is known as abstract class. It can have abstract methods (methods without body) as well as concrete methods (regular methods with body). A normal class (non-abstract class) cannot have abstract methods.
An abstract class cannot be instantiated, which means you are not allowed to create an object of it.
Abstract class declaration

An abstract class outlines the methods but not necessarily implements all the methods.
```
//Declaration using abstract keyword
 abstract class A{
   //This is abstract method
   abstract void myMethod();

   //This is concrete method with body
    void anotherMethod(){
      //Does something
   }
}
```


## Rules :

Note 1: As we seen in the above example, there are cases when it is difficult or often unnecessary to implement all the methods in parent class. In these cases, we can declare the parent class as abstract, which makes it a special class which is not complete on its own. A class derived from the abstract class must implement all those methods that are declared as abstract in the parent class.

Note 2: Abstract class cannot be instantiated which means you cannot create the object of it. To use this class, you need to create another class that extends this this class and provides the implementation of abstract methods, then you can use the object of that child class to call non-abstract methods of parent class as well as implemented methods(those that were abstract in parent but implemented in child class).

Note 3: If a child does not implement all the abstract methods of abstract parent class, then the child class must need to be declared abstract as well.

## Interface :

Interface looks like a class but it is not a class. An interface can have methods and variables just like the class but the methods declared in interface are by default abstract (only method signature, no body, see: Java abstract method). Also, the variables declared in an interface are public, static & final by default.

## What is the use of interface : 

As mentioned above they are used for full abstraction. Since methods in interfaces do not have body, they have to be implemented by the class before you can access them. The class that implements interface must implement all the methods of that interface. Also, java programming language does not allow you to extend more than one class, However you can implement more than one interfaces in your class.

Syntax:

Interfaces are declared by specifying a keyword “interface”.

## Example :
```
interface MyInterface
{
   /* All the methods are public abstract by default
    * As you see they have no body
    */
   public void method1();
   public void method2();
}
```


# EXCEPTION HANDLING :

Exception handling is one of the most important feature of java programming that allows us to handle the runtime errors caused by exceptions.

## What is an exception : 

An Exception is an unwanted event that interrupts the normal flow of the program. When an exception occurs program execution gets terminated. In such cases we get a system generated error message. The good thing about exceptions is that they can be handled in Java. By handling the exceptions we can provide a meaningful message to the user about the issue rather than a system generated message, which may not be understandable to a user.

There can be several reasons that can cause a program to throw exception. 

For example: Opening a non-existing file in your program, Network connection problem, bad input data provided by user etc

## Exception handling :

If an exception occurs, which has not been handled by programmer then program execution gets terminated and a system generated error message is shown to the user.
Exception handling ensures that the flow of the program doesn’t break when an exception occurs. For example, if a program has bunch of statements and an exception occurs midway after executing certain statements then the statements after the exception will not execute and the program will terminate abruptly.
By handling we make sure that all the statements execute and the flow of program doesn’t break.

## Difference between error and exception :

Errors indicate that something severe enough has gone wrong, the application should crash rather than try to handle the error.
Exceptions are events that occurs in the code. A programmer can handle such conditions and take necessary corrective actions.

 Few examples:
 
NullPointerException – When you try to use a reference that points to null.

ArithmeticException – When bad data is provided by user, for example, when you try to divide a number by zero this exception occurs because dividing a number by zero is undefined.

ArrayIndexOutOfBoundsException – When you try to access the elements of an array out of its bounds, for example array size is 5 (which means it has five elements) and you are trying to access the 10th element.


## Types of exceptions :

There are two types of exceptions in Java:

1)Checked exceptions

2)Unchecked exceptions

## Checked exceptions :

All exceptions other than Runtime Exceptions are known as Checked exceptions as the compiler checks them during compilation to see whether the programmer has handled them or not. If these exceptions are not handled/declared in the program, you will get compilation error. For example, SQLException, IOException, ClassNotFoundException etc.

## Unchecked Exceptions :

Runtime Exceptions are also known as Unchecked Exceptions. These exceptions are not checked at compile-time so compiler does not check whether the programmer has handled them or not but it’s the responsibility of the programmer to handle these exceptions and provide a safe exit. For example, ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException etc.Compiler will never force you to catch such exception or force you to declare it in the method using throws keyword.

# MULTI THREADING 

A thread is a light-weight smallest part of a process that can run concurrently with the other parts(other threads) of the same process. Threads are independent because they all have separate path of execution that’s the reason if an exception occurs in one thread, it doesn’t affect the execution of other threads. All threads of a process share the common memory. The process of executing multiple threads simultaneously is known as multithreading.

1.The main purpose of multithreading is to provide simultaneous execution of two or more parts of a program to maximum utilize the CPU time. A multithreaded program contains two or more parts that can run concurrently. Each such part of a program called thread.

2. Threads are lightweight sub- processes, they share the common memory space. In Multithreaded environment, programs that are benefited from multithreading, utilize the maximum CPU time so that the idle time can be kept to minimum.

3. A thread can be in one of the following states:

NEW – A thread that has not yet started is in this state.

RUNNABLE – A thread executing in the Java virtual machine is in this state.

BLOCKED – A thread that is blocked waiting for a monitor lock is in this state.

WAITING – A thread that is waiting indefinitely for another thread to perform a particular action is in this state.

TIMED_WAITING – A thread that is waiting for another thread to perform an action for up to a specified waiting time is in this state.

TERMINATED – A thread that has exited is in this state.

A thread can be in only one state at a given point in time.

## Creating a thread in Java :

There are two ways to create a thread in Java:

1) By extending Thread class.

2) By implementing Runnable interface.

Before we begin with the programs(code) of creating threads, let’s have a look at these methods of Thread class. We have used few of these methods in the example below.

•	getName(): It is used for Obtaining a thread’s name

•	getPriority(): Obtain a thread’s priority

•	isAlive(): Determine if a thread is still running

•	join(): Wait for a thread to terminate

•	run(): Entry point for the thread

•	sleep(): suspend a thread for a period of time

•	start(): start a thread by calling its run() method

## Thread class and Runnable interface :

A thread can be defined in two ways. First, by extending a Thread class that has already implemented a Runnable interface. Second, by directly implementing a Runnable interface. When you define a thread by extending Thread class you have to override the run() method in Thread class. When you define a thread implementing a Runnable interface you have to implement the only run() method of Runnable interface. 

The basic difference between Thread and Runnable is that each thread defined by extending Thread class creates a unique object and get associated with that object. On the other hand, each thread defined by implementing Runnable interface shares the same object.

## Thread :

Thread is a class in java.lang package. The Thread class extends an Object class, and it implements Runnable interfaces. The Thread class has constructors and methods to create and operate on the thread. When we create multiple threads, each thread creates a unique object and get associated with that object. If you create a thread extending Thread class, further you can not extend any other class as java does not support multiple inheritance.
So, you should choose to extend Thread class only when you also want to override some other methods of Thread class. 

## Example :
```
class MultithreadingDemo extends Thread{  
  public void run(){  
    System.out.println("My thread is in running state.");  
  }   
  public static void main(String args[]){  
     MultithreadingDemo obj=new MultithreadingDemo();   
     obj.start();  
  }  
}
```

## Output:
My thread is in running state.


## Runnable Interface :
Runnable is an interface in java.lang package. Implementing Runnable interface we can define a thread. Runnable interface has a single method run(), which is implemented by the class that implements Runnable interface. When you choose to define thread implementing a Runnable interface you still have a choice to extend any other class. When you create multiple threads by implementing Runnable interface, each thread shares the same runnable instance.

## Example :
```
class MultithreadingDemo implements Runnable{  
  public void run(){  
    System.out.println("My thread is in running state.");  
  }   
  public static void main(String args[]){  
     MultithreadingDemo obj=new MultithreadingDemo();  
     Thread tobj =new Thread(obj);  
     tobj.start();  
 }  
}
```

## Output:
My thread is in running state.
