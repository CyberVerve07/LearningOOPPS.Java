# Java OOP Interview Guide

## Interview Questions & Answers

---

## Part 1: Method Overriding vs Threads

### Q1. What is the difference between Method Overriding and Threads?

**Method Overriding:**
- Method overriding is a compile-time concept related to Object-Oriented Programming (OOP)
- It allows a child class to provide a specific implementation of a method that is already defined in the parent class
- Used to achieve runtime polymorphism
- Works within class hierarchy (parent-child relationship)
- Example: When a Dog class overrides the makeSound() method from Animal class

**Threads:**
- Threads are related to concurrent execution and multithreading
- A thread is a lightweight process that executes code independently
- Used to execute multiple tasks concurrently
- Threads run parallel to each other in the JVM
- Example: Creating multiple threads to handle different tasks simultaneously

### Q2. Can we Override the run() method in Java?

**Answer: Yes, we can override the run() method**

The run() method must be overridden when creating a custom thread. There are two ways to create threads:

1. **Extending Thread Class:**
```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread is running");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start();  // This calls run() internally
    }
}
```

2. **Implementing Runnable Interface:**
```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Thread is running");
    }
}

public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(new MyRunnable());
        thread.start();
    }
}
```

### Q3. What happens if we don't override the run() method?

**Answer: Nothing happens**

- The compiler will not show any error
- The thread will start but execute an empty run() method from the Thread class
- You will get no output
- The thread completes immediately without doing any work

**Example:**
```java
class MyThread extends Thread {
    // Not overriding run() method
}

public class Main {
    public static void main(String[] args) {
        System.out.println("Started Main");
        MyThread thread = new MyThread();
        thread.start();
        System.out.println("Ended Main");
    }
}
```

**Output:**
```
Started Main
Ended Main
```

### Q4. What is the difference between start() and run() method?

| Feature | start() | run() |
|---------|---------|-------|
| Creates New Thread | Yes | No |
| Executes in | New thread | Current/Main thread |
| Method Type | Native method | Normal method |
| Multiple Calls | Can be called only once | Can be called multiple times |
| Purpose | Initiates thread execution | Contains thread logic |

**Important Note:** 
- Calling start() method internally calls the run() method in a new thread
- If you call run() directly, it executes in the current thread (Main thread) without creating a new thread

### Q5. Can we Override the start() method?

**Answer: No, you should not override the start() method**

If you override the start() method:
- No new thread will be created
- The run() method will not be called
- No thread initialization will happen
- The overridden start() method will simply execute in the main thread like a normal method

### Q6. What is the difference between Method Overloading and Method Overriding?

| Feature | Overloading | Overriding |
|---------|-------------|-----------|
| Type | Static Polymorphism | Runtime Polymorphism |
| Location | Same class | Parent and child classes |
| Method Signature | Must be different (parameters) | Must be same (parameters) |
| Inheritance | Not required | Required |
| Compile Time | Resolved at compile time | Resolved at runtime |
| Return Type | Can be different | Must be same or covariant |

### Q7. Can we Overload the run() method?

**Answer: Yes, we can overload run() method**

However, when you call start(), only the parameterless run() method (the one we override from Thread class) will be called by the JVM to execute the thread.

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("No parameter run() - executed by thread");
    }
    
    public void run(String message) {
        System.out.println("Overloaded run() with parameter: " + message);
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start();  // Calls run() with no parameters
        thread.run("Manual call");  // Manually call overloaded method
    }
}
```

**Output:**
```
No parameter run() - executed by thread
Overloaded run() with parameter: Manual call
```

### Q8. What will happen if we override start() method instead of run()?

```java
class MyThread extends Thread {
    public void start() {
        System.out.println("Override start() method");
    }
    
    public void run() {
        System.out.println("run() method");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start();  // Calls overridden start() in main thread
    }
}
```

**Output:**
```
Override start() method
```

Notice that run() method is never called because we overrode start() method without calling super.start().

---

## Part 2: Multilevel Inheritance in Java

### Q. Does Java support Multilevel Inheritance?

**Answer: YES, Java DOES support Multilevel Inheritance**

Multilevel inheritance is when a class inherits from another class, which itself inherits from a third class. This creates a chain of inheritance.

### Example of Multilevel Inheritance:

```java
// Level 1: Grandparent class
class Animal {
    public void eat() {
        System.out.println("Animal eats");
    }
}

// Level 2: Parent class (inherits from Animal)
class Dog extends Animal {
    public void bark() {
        System.out.println("Dog barks");
    }
}

// Level 3: Child class (inherits from Dog)
class Puppy extends Dog {
    public void play() {
        System.out.println("Puppy plays");
    }
}

public class Main {
    public static void main(String[] args) {
        Puppy puppy = new Puppy();
        puppy.eat();   // From Animal class
        puppy.bark();  // From Dog class
        puppy.play();  // From Puppy class
    }
}
```

**Output:**
```
Animal eats
Dog barks
Puppy plays
```

### What Java DOES NOT Support: Multiple Inheritance

**Answer: Java does NOT support Multiple Inheritance with classes**

Multiple inheritance is when a class inherits from more than one parent class directly. Java does NOT allow this.

```java
// This will NOT compile in Java
class Dog extends Animal, Pet {  // ERROR: Not allowed
    // ...
}
```

### Why Java does NOT support Multiple Inheritance?

1. **Diamond Problem:** When two classes have a common ancestor and both have the same method, the child class faces ambiguity about which method to use.

2. **Ambiguity:** If class C inherits from both class A and class B, and both have the same method check(), which implementation should C use?

3. **Complexity:** Multiple inheritance makes the code complex and hard to maintain

4. **Simpler Design:** Java focuses on simplicity and clarity

**Example of Diamond Problem:**
```
      Animal
       / \
      /   \
    Dog   Pet
      \   /
       \ /
      ServiceDog
```

If both Dog and Pet have the same method, ServiceDog won't know which one to use.

### How to Achieve Multiple Inheritance in Java?

**Solution 1: Using Interfaces**

```java
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

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();
        dog.play();
    }
}
```

**Solution 2: Using Composition**

```java
class Animal {
    public void eat() {
        System.out.println("Animal eats");
    }
}

class Pet {
    public void play() {
        System.out.println("Pet plays");
    }
}

class Dog {
    private Animal animal = new Animal();
    private Pet pet = new Pet();
    
    public void eat() {
        animal.eat();
    }
    
    public void play() {
        pet.play();
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();
        dog.play();
    }
}
```

---

## Summary

| Concept | Details |
|---------|---------|
| Method Overriding | Child class provides specific implementation of parent method |
| Threads | Independent execution paths for concurrent task execution |
| run() override | MUST override to define thread logic |
| start() method | Creates new thread and calls run() internally |
| Multilevel Inheritance | SUPPORTED - Chain of inheritance (A → B → C) |
| Multiple Inheritance | NOT SUPPORTED with classes, use Interfaces instead |
| Diamond Problem | Reason why multiple inheritance is not supported |

---

## Key Interview Tips

1. Always call **start()** method to create a new thread, not run()
2. You must **override run()** method to define thread behavior
3. Don't override the **start()** method unless you have specific reason
4. Java supports **single inheritance with classes** but multiple inheritance with **interfaces**
5. Multilevel inheritance is **fully supported** and creates a clean hierarchy
6. Use **Interfaces** when you need multiple inheritance
7. Use **Composition** for complex inheritance scenarios

