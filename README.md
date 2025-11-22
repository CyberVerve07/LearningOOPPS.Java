Java OOP Concepts - Complete Learning Repository
📚 Overview
This repository contains comprehensive Java Object-Oriented Programming (OOP) concepts with practical examples, code implementations, and interview preparation materials. It covers the four pillars of OOP, inheritance patterns, multithreading, and advanced concepts with detailed explanations and working code examples.

📋 Table of Contents
What is OOP?

Four Pillars of OOP

Code Examples

Inheritance in Java

Method Overriding vs Threads

Interview Questions

Getting Started

Contributing

What is OOP?
Object-Oriented Programming (OOP) is a programming paradigm that uses objects and classes to structure code. It promotes code reusability, maintainability, and security through its core principles.

Key Benefits:

Code Reusability

Better Organization and Structure

Improved Security

Easier Maintenance

Real-world Modeling

Four Pillars of OOP
1. Encapsulation
Encapsulation is the bundling of data (variables) and methods (functions) into a single unit called a class. It hides internal implementation details and provides controlled access through getter and setter methods.

Key Points:

Data hiding through private members

Access control using public, private, protected, and default modifiers

Getter and setter methods for controlled access

Improves data security and prevents unauthorized access

Example Code:

java
class Student {
    private String name;
    private int rollNo;
    private int marks;
    
    // Getter methods
    public String getName() {
        return name;
    }
    
    public int getRollNo() {
        return rollNo;
    }
    
    public int getMarks() {
        return marks;
    }
    
    // Setter methods with validation
    public void setName(String newName) {
        if (newName != null && !newName.isEmpty()) {
            name = newName;
        }
    }
    
    public void setRollNo(int newRollNo) {
        if (newRollNo > 0) {
            rollNo = newRollNo;
        }
    }
    
    public void setMarks(int newMarks) {
        if (newMarks >= 0 && newMarks <= 100) {
            marks = newMarks;
        }
    }
}
2. Inheritance
Inheritance allows a class to inherit properties and methods from another class. The class that inherits is called the child class, and the class being inherited from is called the parent class.

Key Points:

Code reusability through parent class methods

Parent-child class relationship (IS-A relationship)

Single inheritance, multilevel inheritance, and hierarchical inheritance

Uses extends keyword for class inheritance

Improves code organization and reduces redundancy

Types of Inheritance:

Single Inheritance: Child inherits from one parent

Multilevel Inheritance: Child inherits from parent, which inherits from grandparent

Hierarchical Inheritance: Multiple children inherit from one parent

Multiple Inheritance with Interfaces: A class implements multiple interfaces

Example Code:

java
class Animal {
    public void eat() {
        System.out.println("Animal eats");
    }
}

class Dog extends Animal {
    public void bark() {
        System.out.println("Dog barks");
    }
}

class Puppy extends Dog {
    public void play() {
        System.out.println("Puppy plays");
    }
}

// Using inheritance
Puppy puppy = new Puppy();
puppy.eat();   // From Animal class
puppy.bark();  // From Dog class
puppy.play();  // From Puppy class
3. Polymorphism
Polymorphism means "many forms." It allows objects to take multiple forms and enables methods to perform different actions based on the object that calls them.

Types of Polymorphism:

Compile-time Polymorphism (Static): Method Overloading

Runtime Polymorphism (Dynamic): Method Overriding

Method Overloading Example:

java
class Calculator {
    // Overloading - same method name, different parameters
    public int add(int a, int b) {
        return a + b;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
    
    public int add(int a, int b, int c) {
        return a + b + c;
    }
}
Method Overriding Example:

java
class Animal {
    public void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Dog barks: Woof Woof");
    }
}

class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Cat meows: Meow Meow");
    }
}

// Runtime polymorphism
Animal myDog = new Dog();
Animal myCat = new Cat();
myDog.makeSound();  // Output: Dog barks: Woof Woof
myCat.makeSound();  // Output: Cat meows: Meow Meow
4. Abstraction
Abstraction is the process of hiding complex implementation details and showing only the necessary features of an object. It helps reduce complexity and improve code clarity.

Key Points:

Hide complex implementation details

Show only essential features

Uses abstract classes and interfaces

Achieved through abstract methods and abstract classes

Improves code readability and reduces complexity

Abstract Class Example:

java
abstract class Shape {
    abstract double area();
    
    public void display() {
        System.out.println("This is a shape");
    }
}

class Rectangle extends Shape {
    private double length;
    private double width;
    
    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }
    
    @Override
    double area() {
        return length * width;
    }
}

class Circle extends Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    double area() {
        return Math.PI * radius * radius;
    }
}

// Using abstraction
Shape rect = new Rectangle(5, 4);
Shape circle = new Circle(3);
System.out.println("Rectangle Area: " + rect.area());
System.out.println("Circle Area: " + circle.area());
Code Examples
Example 1: Single Inheritance
java
class Animal {
    String name;
    
    public void eat() {
        System.out.println("I can eat");
    }
}

class Dog extends Animal {
    public void bark() {
        System.out.println("I can bark");
    }
    
    public void display() {
        System.out.println("My name is " + name);
    }
}

public class Main {
    public static void main(String[] args) {
        Dog labrador = new Dog();
        labrador.name = "Rohu";
        labrador.display();
        labrador.eat();
        labrador.bark();
    }
}
Output:

text
My name is Rohu
I can eat
I can bark
Example 2: Multilevel Inheritance
java
class Vehicle {
    public void start() {
        System.out.println("Vehicle is starting");
    }
}

class Car extends Vehicle {
    public void drive() {
        System.out.println("Car is driving");
    }
}

class SportsCar extends Car {
    public void turboMode() {
        System.out.println("Turbo mode activated!");
    }
}

public class Main {
    public static void main(String[] args) {
        SportsCar myCar = new SportsCar();
        myCar.start();       // Vehicle class method
        myCar.drive();       // Car class method
        myCar.turboMode();   // SportsCar class method
    }
}
Output:

text
Vehicle is starting
Car is driving
Turbo mode activated!
Example 3: Method Overriding (Polymorphism)
java
class Animal {
    public void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Dog barks: Woof Woof");
    }
}

class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Cat meows: Meow Meow");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal();
        Animal myDog = new Dog();
        Animal myCat = new Cat();
        
        myAnimal.makeSound();
        myDog.makeSound();
        myCat.makeSound();
    }
}
Output:

text
Animal makes a sound
Dog barks: Woof Woof
Cat meows: Meow Meow
Example 4: Encapsulation
java
class BankAccount {
    private double balance;
    private String accountHolder;
    
    public BankAccount(String accountHolder, double initialBalance) {
        this.accountHolder = accountHolder;
        this.balance = initialBalance;
    }
    
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: " + amount);
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: " + amount);
        } else {
            System.out.println("Invalid withdrawal amount");
        }
    }
    
    public double getBalance() {
        return balance;
    }
    
    public String getAccountHolder() {
        return accountHolder;
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("Raj", 5000);
        account.deposit(2000);
        account.withdraw(1000);
        System.out.println("Current Balance: " + account.getBalance());
    }
}
Output:

text
Deposited: 2000.0
Withdrawn: 1000.0
Current Balance: 6000.0
Example 5: Abstraction with Interface
java
interface DatabaseConnection {
    void connect();
    void disconnect();
    void executeQuery(String query);
}

class MySQLConnection implements DatabaseConnection {
    @Override
    public void connect() {
        System.out.println("Connected to MySQL database");
    }
    
    @Override
    public void disconnect() {
        System.out.println("Disconnected from MySQL database");
    }
    
    @Override
    public void executeQuery(String query) {
        System.out.println("Executing MySQL query: " + query);
    }
}

class MongoDBConnection implements DatabaseConnection {
    @Override
    public void connect() {
        System.out.println("Connected to MongoDB");
    }
    
    @Override
    public void disconnect() {
        System.out.println("Disconnected from MongoDB");
    }
    
    @Override
    public void executeQuery(String query) {
        System.out.println("Executing MongoDB query: " + query);
    }
}

public class Main {
    public static void main(String[] args) {
        DatabaseConnection mysql = new MySQLConnection();
        mysql.connect();
        mysql.executeQuery("SELECT * FROM users");
        mysql.disconnect();
        
        DatabaseConnection mongodb = new MongoDBConnection();
        mongodb.connect();
        mongodb.executeQuery("db.users.find()");
        mongodb.disconnect();
    }
}
Output:

text
Connected to MySQL database
Executing MySQL query: SELECT * FROM users
Disconnected from MySQL database
Connected to MongoDB
Executing MongoDB query: db.users.find()
Disconnected from MongoDB
Inheritance in Java
Types of Inheritance
Type	Description	Example
Single Inheritance	A class inherits from one parent class	class Dog extends Animal
Multilevel Inheritance	A class inherits from another class, which inherits from a third class	class Puppy extends Dog extends Animal
Hierarchical Inheritance	Multiple classes inherit from a single parent class	Dog and Cat both extend Animal
Multiple Inheritance (Interfaces)	A class implements multiple interfaces	class Dog implements Animal, Pet
Important Notes
Java DOES support Multilevel Inheritance ✅

Java DOES NOT support Multiple Inheritance with classes ❌

Use interfaces to achieve multiple inheritance behavior

Use composition for complex inheritance scenarios

The super keyword is used to call parent class methods

Diamond Problem
The Diamond Problem occurs in multiple inheritance when a class inherits from two classes that share a common ancestor.

text
      Animal
       / \
      /   \
    Dog   Pet
      \   /
       \ /
    ServiceDog
If both Dog and Pet have the same method, ServiceDog faces ambiguity. Java avoids this by not supporting multiple inheritance with classes.

Solution: Use interfaces

java
interface Animal {
    void eat();
}

interface Pet {
    void play();
}

class Dog implements Animal, Pet {
    @Override
    public void eat() {
        System.out.println("Dog eats");
    }
    
    @Override
    public void play() {
        System.out.println("Dog plays");
    }
}
Method Overriding vs Threads
Method Overriding
Method overriding is an OOP concept where a child class provides a specific implementation of a method that is already defined in the parent class. It enables runtime polymorphism.

Key Characteristics:

Works within class hierarchy (parent-child relationship)

Used to achieve runtime polymorphism

Method signature must be same as parent class

Uses @Override annotation

Resolved at runtime

Threads
Threads are lightweight processes that enable concurrent execution in Java. A thread is an independent path of execution within a program.

Key Characteristics:

Used for concurrent execution of multiple tasks

Threads run parallel within JVM

Related to multithreading and concurrency

Not related to OOP class hierarchy

Improves application responsiveness

Important Distinctions
Aspect	Method Overriding	Threads
Purpose	Achieve polymorphism	Execute tasks concurrently
Related to	OOP concepts	Concurrency
Involves	Parent-child classes	Independent execution paths
Used for	Different implementations	Parallel task execution
Location	Class hierarchy	JVM process
run() Method and Threads
Can we override the run() method?
Yes, the run() method MUST be overridden when creating a custom thread.

java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread is running");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start();  // Calls run() internally
    }
}
Difference between start() and run():

Method	Purpose	Creates New Thread	Executes In
start()	Initiates thread execution	Yes	New thread
run()	Contains thread logic	No	Current thread
Important: Always call start() to create a new thread. Calling run() directly executes it in the current thread without creating a new thread.

Can we override start()?
No, you should NOT override the start() method. If you do:

No new thread will be created

The thread initialization will not happen

The overridden start() method will execute in the main thread like a normal method

Interview Questions
OOP Concepts
Q1. What are the four pillars of OOP?
A. Encapsulation, Inheritance, Polymorphism, and Abstraction.

Q2. What is the difference between abstraction and encapsulation?
A. Abstraction hides complexity by showing only essential features, while encapsulation bundles data and methods together and controls access through access modifiers.

Q3. Can we instantiate an abstract class?
A. No, abstract classes cannot be instantiated. They must be extended by a concrete class.

Q4. What is the difference between method overloading and method overriding?
A. Method overloading occurs in the same class with different parameters (compile-time), while method overriding occurs in parent-child classes with the same parameters (runtime).

Inheritance
Q5. Does Java support multiple inheritance with classes?
A. No, Java does not support multiple inheritance with classes due to the diamond problem. However, it supports multiple inheritance through interfaces.

Q6. Does Java support multilevel inheritance?
A. Yes, Java fully supports multilevel inheritance where a class can inherit from another class that inherits from a third class.

Q7. What is the diamond problem?
A. The diamond problem occurs when a class inherits from two classes that share a common ancestor, causing ambiguity about which method to use.

Threads and Overriding
Q8. Can we override the run() method?
A. Yes, the run() method must be overridden to define thread behavior. However, you should not override the start() method.

Q9. What is the difference between start() and run() methods?
A. start() creates a new thread and calls run() internally, while run() contains the thread logic and executes in the calling thread if invoked directly.

Q10. What happens if we don't override the run() method?
A. The thread will start but execute an empty run() method without performing any tasks.

Getting Started
Prerequisites
Java Development Kit (JDK) 8 or higher

Any Java IDE (Eclipse, IntelliJ IDEA, VS Code)

Git (for cloning the repository)

Installation
Clone the repository:

bash
git clone https://github.com/yourusername/java-oops-concepts.git
cd java-oops-concepts
Compile the code:

bash
javac src/*.java
Run examples:

bash
java -cp src Main
Project Structure
text
java-oops-concepts/
├── src/
│   ├── Encapsulation.java
│   ├── Inheritance.java
│   ├── Polymorphism.java
│   ├── Abstraction.java
│   ├── Threads.java
│   └── Main.java
├── README.md
├── LICENSE
└── .gitignore
Key Takeaways
✅ Encapsulation: Bundle data and methods, control access with modifiers

✅ Inheritance: Reuse code through parent-child relationships (single, multilevel, hierarchical)

✅ Polymorphism: Objects can take multiple forms (overloading, overriding)

✅ Abstraction: Hide complexity, show only essential features

✅ Java supports multilevel inheritance but NOT multiple inheritance with classes

✅ Use interfaces for multiple inheritance behavior

✅ Use composition for complex inheritance scenarios

✅ Override run() method for threads, NOT start() method

✅ Call start() method to create new thread, NOT run() directly

Contributing
Contributions are welcome! Please follow these steps:

Fork the repository

Create your feature branch (git checkout -b feature/AmazingFeature)

Commit your changes (git commit -m 'Add some AmazingFeature')

Push to the branch (git push origin feature/AmazingFeature)

Open a Pull Request

License
This project is licensed free to open source learn

References: GeeksforGeeks, TutorialsPoint, Oracle Java Documentation

Inspired by real-world development practices
