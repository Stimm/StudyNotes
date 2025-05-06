- What is .Net and how does it work
- What is the CLR, and why is it important?
- What are the differences between .NET Framework, .NET Core, and .NET 5+?
- What is CIL (Common Intermediate Language)?
- What is the difference between managed and unmanaged code?
- What are value types and reference types in C#
-  What is a delegate in C#, and how is it used?
- What is a class? 
- What are the main concepts of object-oriented programming? 
- Explain Encapsulation 
- What is abstraction? 
- What is Inheritance in C#?
- What is polymorphism? 
- What is an object? 
- What is a constructor, and what are its different types? 
- What is a destructor in C#? 
- Is C# code managed or unmanaged code?
- What are value types and reference types? 
- What are namespaces, and is that compulsory? 
- Explain types of comments in c# with examples. 
- What is an interface? Give an example. 
- How to implement multiple interfaces with the same method name in the same class? 
- What is the virtual method, and how is it different from the abstract method?
- What is method overloading and method overriding? 
- What is the static keyword? 
- Can we use “this” with the static class? 
- What is the difference between constants and read-only? 
- What is the difference between string and string builder in C#? 
- Explain the “continue” and “break” statement. 
- What are boxing and unboxing? 
- What is a sealed class? 
- What is a partial class? 
- What is enum?
- What is dependency injection, and how can it be achieved? 
- The “using” statement. 
- What are the access modifiers? 
- Explain each type. 
- What are delegates? 
- What are the different types of delegates? 
- What is an array?
- Explain Single and multi-dimensional arrays. 
- What is the difference between the System.Array.CopyTo() and System.Array.Clone() ? 
- What is the difference between array and arraylist? 
- What is a jagged array in C#? 
- What is the difference between struct and class? 
- What is the difference between throw and throw ex? 
- Explain the difference between finally and finalize block? 
- What are Anonymous types in C#? 
- What is multithreading, and what are its different states? 
- How is exception handling done in C#? 
- What are the custom exceptions? 
- What is LINQ in C#? 
- What is serialization? 
- What are generics in c#? 
- What is reflection? 
- How to use nullable types?
- Which is the parent class of all classes which we create in C
- Explain code compilation in C#
- Differences between .net Framework and .net Core
- What is the difference between async and await
- What is dependency injection in .NET, and why is it used?
- What are generics in C#?
- What is LINQ, and how does it work
- What is the difference between IEnurmeral, IQuarable, List
- What is reflection in C#?
- What is boxing and unboxing
- What is middleware in ASP.NET Core?
- What are async streams, and how do they work?
- What are microservices, and how does .NET support them?
- he acronym SOLID stands for
- Patterns*-

[[cSharp coding questions]] 


##### What is .NET, and how does it work?
.Net is a cross platform framework developed my MC. Its designed to work on desktop, movbil, web and cloud.

Languages: c# f# and vb.net

Compiling: Instead of compiling directly into machien instructions .Net applications compile into a commen intermediate language (CLI). Then the Commen language runtime (CLR)
translates the cli into machien code at runtime, allowing for cross-platform execution.

CLR(Common Language Runtime): Executes .NET apppl;ations, manages memory, security and performance

BCL (Base Class Libary) a collection of reusable libaries for file handeling, collections and more

JIT (Just in time) compiler: Converts CLI into optomized machine code at runtime

##### What is the CLR, and why is it important?
The Common language language Runtime (CLR) is the execution enviorment for .NET applications. IT provides 
automatic memory managment 
- security 
- performance optimizations 

How it works
- Code written in a .Net language compiles into Common intermediate Language (CIL)
- The Just-in-time compiler translates the CIL into machien code at runtime 
- The Garbage collector Automaticly manages memory by reclaiming unused objects 
- The CLR enforces security policies and prevents unauthorized memory

##### What are the differences between .NET Framework, .NET Core, and .NET 5+?
Net evloved from a windows only baed solution to encompous other platforms including cloud the three main versions are 

- .NET Framework: The original framework only suports windows enviorments such as Windows, WinForms and olfer ASP.NET. No longer recieves major updates but because if its use in Finteck still recieves lots of love
- NET Core: is the first cross-platform frame work, runs on desktop, mobile, ios and cloud. Suports docker, Kuberneties and microservices 
- .Net 5+ is really the contuiniation of .Net Core I think we are at 8 now? 

##### What is CIL (Common Intermediate Language)?
When you compile your code it dosent turn into machiean code right a way, insterad its converted into the CIL or Common Intermediat Language which is then picked up by the CLR

IT allows for
- Cross platform compatability: Any .NET language can run on any enviorment
- Language interprperbility: All .Net languages can interact seamlessly 

##### What is the difference between managed and unmanaged code?
Managed code is code that is handled with in the CLR. The CLR handles all memory allocation, security and garbage collection. It frees up and assigned memory as needed and prevents out side processes from touching your memory.

Unmanaged is code that is run out side of the CLR and requires devlopers to design there code to manage these acpects.,

###### What is garbage collection in .NET, and how does it work?
Garbage collection in .NET is a automatic process handled by the CLR to insure that memory is not wasted on unused objects. It runs in 3 stages

- Scanning: Finds unuesed objects
- Sweeping: Removes the objects
- Compacting: Reorganises the available memory

There are ways to manuualy trigger Garbage collection are are part of the Systems.GC GC.Collect()

##### What are value types and reference types in C

Value types
- Store the value direactly into memory
- When assigned to a new varabiel a copy of the value is made
- Modifying one variable dose not affect eh other
The Value types are
- int
- float
- char
- bool
- struct
- enum

Reference types are types that store a copy of the value as well as its posiction in memmory. They are a referance to a place in memory an example of this would be
- String
- Any Class/Object

##### What is a delegate in C#, and how is it used?
Delagates a type that can act as a referance to a method.

For instance you could create a delagate for a method that would take in a string and then go on to create that method. you can then assign that method to that delagate and use that instead of calling the method. Its usefull with event handeling and callbacks.

MultyCasting is when you chain delagates together to fire one after another.

##### What is a class.
A class is a template to create an Object. It contains attributes and methods. We can create many instances from a single class.


##### What are the main concepts of object-oriented programming? ** 
- **Encapsulation, 
- **Abstraction, 
- **Polymorphism,** 
- **Inheritance** 
are the main concepts of object-oriented programming.

##### Explain Encapsulation
Enchapsulaton is the wraping functions and data members together in one class. I.e Getters and Setters. This prevents unwanted changes to the data from out side of the function.

Set attrabutes to be private and make available getters and setter to manipulate them.


##### Explain abstraction
Abstraction is the process of only making visable the attrabutes of a class that we want made available to mutation. 

it focuses on provididing access to spesfic functionality with out exposing how the functinality works. An example of this would be having one public method of a class that calls private methods of that class.

##### What is polymorphism
Polymorphisem refers to The same method but differet implamentation. There are two forms of Polymorphisem 
Compile-Time Polymorphisem: The overloading of Methods

Run-Time Polymorphisem: The OverRiding of methods 

##### What Is Inheritance
Inheritance is the pattern of taking Attrabutes and methods from another defined class(Parent class).

The Class that recieves these attrabutes and mehods is normlay refered to as the subclass or child class.

##### What is an Object
A Object is a instance of a class of which we access the functions of that class. Classes are created with the "New" keyword.

##### What is a constructer and what are the diffrent types
A constructor is unique method for every class which handles the creation or initialization of a object. Regardless of not if you include a constructor one will be generated.

There are five types of constructors

1. Default Constructors
2. Paramatised Constructors
3. Copy Constructors
4. Static Constructors 
5. Private Constructors


##### What is a destructor
A destructor calls for garbage collection on a object to have it removed from memory.
Normaly this is handled automaticaly but you can trigger it manualy.

##### Is C# code managed or unmanaged code?
c# is managed because common language runtime compiles the code to intermediate language. 

##### What are value types and reference types?
Value types contain the value direactly: bool, byte, int, char, decimal. 
Referance types contain a reference in memory where the value is stored: String, classes, delegates.

##### What are namespaces, and is that compulsory?
Namespaces is a way of organizing classes of the same group or functinality under the same name. We can call it a module. Although it is not compulsory to put classes in a namespace.

##### Explain types of comments in c# with examples.
Single line comments //
Multyline comments /*  
xml comments ///

##### What is an interface? Give an example.
A interface is another form of abstraction. Interfaces them selves only have declarations and not definitions so only method stubs. Classes that implement a interface must create there own implementation of any method declared in the interface.  Interfaces are use full in acting as contracts for classes and allow you to group classes.

##### What is the virtual method, and how is it different from the abstract method?

A virtual method must have a default implementation, we can override this virtual method using the override keyword in the derived class

The ambstract method is with out implementation and is created inside the abstractr class only,. in the case of abstrract class, the class iderived from the abstract clas must have an implementation of the abstract method.

#####  What is method overloading and method overriding
Method overload is when a method can have the same name but different signatures. 

Overriding is when you overide an existing method from a parent class with a new method in the child class

##### What is the static keyword?
We use the static keyword to create static classes, static methods or static proporities.

Static means that when we create a static class that there can only be one instance ofd that class, its members and its methods.

##### Can we use 'This' when working with static classes.
No, as there is no other instance of a static class just the static class.

##### What is the difference between constants and read-only?
Constat attrabutes need to be asigned at time of decloration. As in they have to be hard code into the Class template and can not be assigned at Object construction.

Readonly can be assigned at both time of decloration or during the construction of a object.

##### What are boxing and unboxing
The conversion of referance types  to value type 


##### What is a Seald class
No need to inherit the class further

##### Partial class
The partial frame work is used for braking down large classes into easer to manageable files

##### Enum
In c# the “enum” keyword is used to declare an enumeration. An enum is a value type. It is a collection of related named constants referred to as an enumerator list. 

An enum type can be any of these (int, float, double, and byte). However, to use it beside int, explicitly casting is required.

To create a numeric constant in the .NET framework enum is used. All the members of the enum are of enum type, and there must be a numeric value for each enum type.

Int is the default type of the enumeration element. By default, the first enumerator has the value 0. The value of each successive enumerator is then increased by 1.

##### What is dependency injection, and how can it be achieved?
Dependency injection is a design pattern. Here, instead of creating an object of a class in another class (dependent class) directly, we are passing the object as an argument in the constructor of the dependent class. It helps to write loosely coupled code and helps to make the code more modular and easy to test.

There are 3 ways to achieve dependency injection.

- Constructor Injection: This is the most commonly used Injection type. In constructor injection, we can pass the dependency into the constructor. We have to make sure that we do not have a default constructor here, and the only one should be a parameterized constructor.

- Property Injection: There are cases when we need the default constructor of a class, so in that case, we can use property injection.

- Method Injection: In method injection, we need to pass the dependency in the method only. When the entire class does not require that dependency, there is no need to implement constructor injection. When we have a dependency on multiple objects, then instead of passing that dependency in the constructor, we pass that dependency in the function itself where it is required.

##### The “using” statement.**


[[How does the internet work]]


##### What are the access modifiers? Explain each type.**

Access modifiers are keywords used to provide accessibility to a class, member, or a function.

Below are its types

- Public: Can be accessed anywhere without any restriction
- Protected: Access is limited up to the class, which inherits this class.
- Internal: Can be accessed only within the current assembly.
- Private: Cannot be accessed outside.

##### **What are delegates?** **

Delegates are like function pointers. It is a reference data type that holds the reference of a method. We use delegates to write generic type-safe functions. All delegates derive from System. Delegate.

A delegate can be declared using the delegate keyword followed by a function signature, as shown below.

The Following are the characteristics of delegates.

- Delegates derive from the System. Delegate class.
- Delegates have a signature as well as return type. A function assigned to delegates must be fit with this signature.
- Delegates can point to instance methods or static.
- Delegate objects, once created, can dynamically invoke the methods it points to at runtime.
- Delegates can call methods synchronously and asynchronously.


##### What are the different types of delegates
- Single Delegate: Single Delegate can invoke a single method.
- Multicast Delegate: Multicast delegates can invoke multiple methods. The delegate method can do multicasting. We can add a method in the delegate instance using + operator, and we can remove a method using – operator. All the methods are invoked in sequence as they are assigned.
- Generic Delegate:  .Net Framework 3.5 Introduces Generic delegates. There is no need to create an instance in a generic delegate.

##### System.Array.CopyTo() and System.Array.Clone()
CopyTo coppies the array to an existing array, Clone creates a new array. 

##### Array v Array list
An array has a set amount of size with a spesfic type while an array list can grow and shirnk and contain any number of types.


##### **What is a jagged array in C#**

A multy dimanttional array.

##### **What is the difference between struct and class?** **

Class and struct are both user-defined but have a significant difference.

**Struct**

- A Struct inherits from System. Value type and so it is a value type.
- It is preferred to use struct when there is a small amount of data. 
- A structure cannot be abstract.
- There is no need to create an object with a new keyword.
- Struct does not have permission to create any default constructor.


##### **What is the difference between throw and throw ex?**

“Throw” statement holds the original error stack of the previous function or function hierarchy. In contrast, “Throw ex” has the stack trace from the throw point.  So it is always advised to use “Throw” because it provides exact error information related to the function and gives you actual trace data of error source.


##### **Explain the difference between finally and finalize block?**

Finally, it is a code block part of execution handling this code block executes irrespective of whether the exception occurs or not.

While the finalize method is called just before garbage collection. The compiler calls this method automatically when not called explicitly in code.

##### **Explain var and dynamic.** **

a Var's type will be set at compile time based on what ever value type it is is set to. 
Dynamic has the ability to change type on the fly

##### **What is multithreading, and what are its different states?**

Any code block in c# runs in a process called a thread, and it is the execution path of the program. Usually, an application runs in a single thread. But multithreading helps to run the application in multiple threads. Using multithreading, we can divide the execution of our process among different threads to execute it simultaneously.

In multithreading, we can create multiple threads and assign particular tasks or put a code block to get executed. In this way, we can run more than one task at a time. This code block executes simultaneously and can save time, and in this way, we can make programs more efficient and fast.

Thread has its lifecycle, which includes various states of thread.

|   |   |   |
|---|---|---|
|Aborted|256|The thread state includes [AbortRequested](https://docs.microsoft.com/en-us/dotnet/api/system.threading.threadstate?view=netcore-3.1#System_Threading_ThreadState_AbortRequested) and the thread is now dead, but its state has not yet changed to [Stopped](https://docs.microsoft.com/en-us/dotnet/api/system.threading.threadstate?view=netcore-3.1#System_Threading_ThreadState_Stopped).|
|AbortRequested|128|The [Abort(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.threading.thread.abort?view=netcore-3.1#System_Threading_Thread_Abort_System_Object_) method has been invoked on the thread, but the thread has not yet received the pending [ThreadAbortException](https://docs.microsoft.com/en-us/dotnet/api/system.threading.threadabortexception?view=netcore-3.1) that will attempt to terminate it.|
|Background|4|The thread is being executed as a background thread, as opposed to a foreground thread. This state is controlled by setting the [IsBackground](https://docs.microsoft.com/en-us/dotnet/api/system.threading.thread.isbackground?view=netcore-3.1#System_Threading_Thread_IsBackground) property.|
|Running|0|The thread has been started and not yet stopped.|
|Stopped|16|The thread has stopped.|
|StopRequested|1|The thread is being requested to stop. This is for internal use only.|
|Suspended|64|The thread has been suspended.|
|SuspendRequested|2|The thread is being requested to suspend.|
|Unstarted|8|The [Start()](https://docs.microsoft.com/en-us/dotnet/api/system.threading.thread.start?view=netcore-3.1#System_Threading_Thread_Start) method has not been invoked on the thread.|
|WaitSleepJoin|32|The thread is blocked. This could be the result of calling [Sleep(Int32)](https://docs.microsoft.com/en-us/dotnet/api/system.threading.thread.sleep?view=netcore-3.1#System_Threading_Thread_Sleep_System_Int32_) or [Join()](https://docs.microsoft.com/en-us/dotnet/api/system.threading.thread.join?view=netcore-3.1#System_Threading_Thread_Join), of requesting a lock – for example, by calling [Enter(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.threading.monitor.enter?view=netcore-3.1#System_Threading_Monitor_Enter_System_Object_) or [Wait(Object, Int32, Boolean)](https://docs.microsoft.com/en-us/dotnet/api/system.threading.monitor.wait?view=netcore-3.1#System_Threading_Monitor_Wait_System_Object_System_Int32_System_Boolean_) – or of waiting on a thread synchronization object such as [ManualResetEvent](https://docs.microsoft.com/en-us/dotnet/api/system.threading.manualresetevent?view=netcore-3.1).|

##### How is exception handling done in C#?

Try, catch, finally, and throw. These are the keywords used to handle the exception.

##### **What are the custom exceptions?**


##### **What is LINQ in C#?** **

Language integrated query is the full form of LINQ. It is a method of querying data using the .net capabilities and c# syntax similar to SQL query.

##### **What is serialization?**

##### **What are generics in c#?**

Generics increase performance, increase type safety, reduce repeated code, and makes reusable code. Using generics, we can create collection classes. It is preferred to use System.Collections.Generic namespace instead of classes such as ArrayList in the System.Collections namespace to create a generic collection.


##### **What is reflection?**

Reflection is when managed code can read its own metadata to find assemblies.

##### **How to use nullable types?**

In c#, we can also assign a null value to the variable. Such types are called nullable types.

##### **Which is the parent class of all classes which we create in C#?**

System.object.

##### **Explain code compilation in C#.**

Below are the steps explaining the code compilation.

- The C# compiler compiles the code into managed code, also called Byte code.
- Then JIT (Just in time compiler) compiles the Byte code into Native or machine language, which is directly executed by CPU.

##### Differences between .net Framework and .net Core 
Key Differences:

- **Platform Support:**
    
    - **.NET Framework:** Primarily for Windows-based applications. 
    - **.NET Core (now .NET):** Cross-platform, supporting Windows, macOS, and Linux. 
    
- **Open Source:**
    
    - **.NET Framework:** Not fully open-source. 
    - **.NET Core (now .NET):** Fully open-source. 
    
- **Performance:**
    
    - **.NET Framework:** Can have performance bottlenecks and scalability limitations. 
    - **.NET Core (now .NET):** Offers superior performance and scalability. 
    
- **Modularity:**
    
    - **.NET Framework:** A monolithic framework with a large dependency footprint. 
    - **.NET Core (now .NET):** More modular and lightweight, allowing for a smaller footprint and quicker deployment. 
    
- **Development Flexibility:**
    
    - **.NET Framework:** Less flexible, with a focus on traditional Windows applications. 
    - **.NET Core (now .NET):** More flexible, supporting various application types, including web apps, microservices, and cloud applications. 
    
- **Target Audience:**
    
    - **.NET Framework:** Ideal for legacy applications and Windows-specific development. 
    - **.NET Core (now .NET):** Best for new projects, microservices, cloud applications, and cross-platform development. 
    
- **Support Lifecycle:**
    
    - **.NET Framework:** Microsoft has ended support for .NET Framework 4.8. 
    - **.NET Core (now .NET):** Microsoft continues to actively develop and support .NET. 
    
- **ASP.NET:**
    
    - **.NET Framework:** Uses ASP.NET Web Forms and ASP.NET Web Pages. 
    - **.NET Core (now .NET):** Uses ASP.NET Core, which is a modern, cross-platform framework for building web applications and APIs. 
    
- **Technologies:**
    
    - **.NET Framework:** Includes technologies like WCF, Web Forms, and Workflow Foundation. 
    - **.NET Core (now .NET):** Focuses on modern features and technologies, including Razor Pages, Blazor, and Minimal APIs.


##### What is the difference between async and await
Systems sometimes need to wait for processes to be completed such as File I/O a Database call or a the result from a resfull call

To prevent systems from freezing out while these processes are being complete we can use Async or await to spin up another thread while the main tread remains active.

We use async to indacate that a method will he handled off the main thread but that alone is not anough to do multy threading. With in the method we have to use the Await call which indacates the start of the asynchronously call; 

Await will pause the exacution of the method untill the result has returned 


##### What is dependency injection in .NET, and why is it used?
Its normal for classes to need to pass in or initeate other classes for them to function as intended. But by hard coding these initeations we cause the classes to become tightly coupled. This can have to main negetie effects 1: code redagitity and 2: issues with testing. 

Dependency injection is the act of passing in classes or what tends to be the case the passing of interfaces of classes during the construction of a class. 

this allows for the class to become some what class agnostic as well as make it easer to mock the injected class for unti testing reasons.



##### What are generics in C#?
in c# we have the ability to create code that works with diffrent data types. an example of this could be the Console.Writeline method. 

In these instances we can use the same methods and class to handle diffrent types.

This helps with 
- Code reusablity
- Type safty: Prevents runtime errors by checking the type at compile time
- Performance: Avoides boxing unboxing

One usefull implamentation of generics is in collections.  and example of this could be Dictonarys where we can simply define what the types are

#####  What is LINQ, and how does it work
Language intergrated query is a c# feature that eases data access with a almost sql like language.

It can do functional operations and in genreal is much easer to read.

a simple example would be the foreach() loop or when access a collection with the .where clause .where(n => n== "Test");

One intresting aspect of LINQ is that they can be defered operations meaning they only run when they are needed.

##### What is the difference between IEnurmeral, IQuarable, List

- IEnurmeral is for itterating over data that is allready in memory. 
- IQuerable is for make DB calls 
- List is a generic collection for storing new data into memory unlike Ienurmeral

##### What is reflection in C#? **
Reflection is gives us the abbility to access and manipulate types, methods and precesses at runtime.

it has four main functions which are 
- Gain access to mata data
- Dynamicly call methods at runtime 
- Creare objects at runtime
- Serilization frameworks
- Dependency injection and testing frameworks

##### What is boxing and unboxing
its the converting to and from value types and reference types

##### What is middleware in ASP.NET Core?

##### What are async streams, and how do they work?

##### What are microservices, and how does .NET support them? **
Microservices is arcetectural pattern where a system is made out of a collection smaller and indapended services. It allows for better 
- Scailability 
- Maintainability
- flexability

Monalithic/Classical systems are build as a singler tightly coupled system and deployed all togthere. Scailability becomes dificult when you may only have one part of you system getting all the trafic at a time.

How dose .Net support microservices
- asp.net: Simplafies the creation of light API's that serve as micro services
- Docker: allows for servers to run in contains, isolated.
- Kuberneties: Helps manage the containerized services, allowing for scailability 
- gPRC: Allows for communcation between servises by useing binary protocol instead of Restful APIS
- Messagebrokers: RabbitMQ, Azure Service Bus, and Kafka are used for messaging, sending events 

How do you publish messages to a kuberneties queue 



##### The acronym SOLID stands for:**

1. **Single Responsibility Principle (SRP):**
    
    - **Definition:** A class should have only one reason to change, meaning it should have only one responsibility.  
        
    - **Goal:** To ensure that a class is focused on a single aspect of the system, making it easier to understand, test, and maintain. Changes to one responsibility will not affect other responsibilities.  
        
    - **Example:** Instead of having a `User` class that handles both user data and email sending, these responsibilities should be separated into a `User` class and an `EmailService` class.
2. **Open/Closed Principle (OCP):**
    
    - **Definition:** Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.  
        
    - **Goal:** To allow adding new functionality without altering existing, well-tested code. This is typically achieved through abstraction and polymorphism.  
        
    - **Example:** Instead of modifying a `Shape` class every time a new shape is introduced, create an abstract `Shape` class or an interface with a method like `calculateArea()`. New shapes (e.g., `Circle`, `Rectangle`) can then extend or implement `Shape` without modifying the original `Shape` class or the code that uses it.
3. **Liskov Substitution Principle (LSP):**
    
    - **Definition:** Subtypes should be substitutable for their base types without altering the correctness of the program.  
        
    - **Goal:** To ensure that any class that is a descendant of a base class can be used in place of the base class without causing unexpected behavior.
    - **Example:** If you have a base class `Bird` with a `fly()` method, a subclass `Penguin` should not be forced to implement `fly()` in a way that doesn't make sense (as penguins don't fly in the traditional sense). A better design might involve separating flying and non-flying birds into different abstractions if their behaviors diverge significantly.  
4. **Interface Segregation Principle (ISP):**
    
    - **Definition:** Clients should not be forced to depend on interfaces they do not use.
    - **Goal:** To avoid creating large, "fat" interfaces that force classes to implement methods they don't need. Smaller, more specific interfaces are preferred.  
        
    - **Example:** Instead of having a single `Worker` interface with methods like `work()`, `eat()`, and `sleep()`, it's better to have separate interfaces like `Workable`, `Eatable`, and `Sleepable`. A robot worker, for instance, would only need to implement `Workable`.
5. **Dependency Inversion Principle (DIP):**
    
    - **Definition:**
        - High-level modules should not depend on low-level modules. Both should depend on abstractions.  
            
        - Abstractions should not depend on details. Details should depend on abstractions.  
            
    - **Goal:** To reduce coupling between modules by making them depend on abstractions (interfaces or abstract classes) rather than concrete implementations. This makes the system more flexible and easier to change.

##### Patterns

###### Creational Patterns – Handling object creation efficiently

- **Singleton** ensures only one instance of a class exists throughout an application.
    
- **Factory Method** provides a way to create objects without specifying their concrete type.

###### Structural Patterns – Organizing relationships between objects

- **Adapter** allows incompatible interfaces to work together
    
- **Decorator** adds behavior dynamically to an object without modifying its structure
	- To implament you need
	- A base Inteface
	- A Concreat class: this takes in the base interface
	- Base Decorator class: Which takes in a instance of the base class.
	- A Derived Decorator class: The child of the base Decorator class witch can be used to add aditional function to the Base class

###### Architectural pattern

- **CQRS** (**C**ommand **Q**uery **R**esponsibility **S**egregation) is a pattern of design where you seprate the read and wright queries of CRUD
- Clean coding arcetucture

###### Behavioural design patterns

- **Mediator** pattern is a further step into DI where we are calling a mediator to handle the injection of classes. This helps decouple classes and prevents curricular logic. We used Query classes that call the actual queries and Handler classes that call the Query classes.

##### What is ASP.NET?
Active server pages is a .Net frame work that gives a simple and versatile aproch for Creating, deploying and running web aplications using the .Net languages. Designed to work with Restfull API's it provides good intergration to css, HTML and Javascript.

##### Write down the features of ASP.NET?****

- Extending the .Net framework
	- Allows for the extention of the .Net frame work to allow the use of .Net libarys for comment web applactions such as MVC, Razor
- Performance
	- High performance when compaired to other frame works on the market
- Backend code
	- Backend code can be written in c#
- Dynamic Pages
	- Razor allows for devloping dynamic web pages and for intergration with Angular and react.
- Suports different Os's


##### What is MVC framework

- Model: The business logic layer
- View: The user interface layer
- Controler: the go between the two other layers

##### What is the differance between ASP.Net MCV and ASP.Net API
- ASP.Net MCV: Is used for creating web applactions and their front ends
	- Accepts only returned information in the form of Json
- ASP.Net Web API: Is used for the creation of RESTfull APIs in a basic and simpley way for handeling communactation between systems. Suports Content negeotation and self-facilitatiing.
	- Accepts different return types based on the Accepts parameter in the headder 


##### What is Server Controle
ASP.Net allows the the controling of Server side values. This allows us to create valadating or dynamic web forms.

##### What is the web.config file
The web.config file is a xml file that exists in the root folder of our applaction.
It containes the configered settings of the websight

##### Which compiler is usesd in ASP.Net
Roslyn

##### What is the Global.asax file ****
- It is a file that exists in the root of a project and is responsoble for handeling and configuring higher level applaction events such as Application_Start, Application_End, Session_Start and Session_end.
- At run time the file is parserd into a dynamicaly created .Net class derived from the HTTP class.
- External users are unable to download or view this file.

##### How many types of Server controle are supported by ASP.Net**

1. HTML Server controls
2. Web Server controles
3. User Controles
4. Valadation Controles

##### What dose post back mean in ASP.Net
Its the proces of presenting a page to the server for processing. Example could be checking the credentials of a user.

##### Difference between Web.config and Machine.config file?****

Machine.config is focused on the running of the server.
web.config is focused on the running of the applaction.
Machine.config is the design configuration file for all the applications in the IIS, but Web. config is a configuration file for a specific application.

##### What is Razor in ASP.NET?
Provides the syntax for building dynamic web pages. Includes Angular and React for allow for SPA

##### What are the types of Authentication in ASP.NET**

- Form Authentication
- Passport Authentication
- Windows Authentication
- Custom Authentication

##### What is Query String in ASP? And what are its advantages and disadvantages
Query strings allow us to pass information from one page to another with the use of & and ?. The down side is that it is limited to 255 characters.

##### Briefly describe the difference between the Web Site and Web Application?
A web applications is an applationt that can be accessd though a browser. Web applactions require authentafiocation and normaly require you to communacate with a backend server.

A Web site is a collection of web pages, images and sound that is accessed thourgh a web browser. A web site can be a single page dynamic applaction or a multy page applaction.

##### Explain Cookies in ASP.NET?
Cookies are small pieces of information that can be sent to and stored in a browser.

##### Explain the purpose of Web Services in ASP.NET?
Web services are accentirly smaller applactions containing methods that be interacted by other Web services.

##### Write a step for Request Flow in ASP.NET MVC framework? **

- Request
	- The request is recieved and then in the Global.asax file route objects are added to the rout table.
- Routing
	- The routing table guids URL's to the correct handler.
	- Routing accores by matching the incoming URL to Urls patterns found in the routing table.
	- The Routing table routs the request to the correct IRouteHandeler based on the matching of the pattern
	- If the pattern is not found then return a 404
- MVC
	- A rout handel will then serve the Http request as acording to the RequestContext
- Controller
	- The controler then decides on which method to be used
- Action executed
	- ActionInvoker will then activate the correct methods. The method recieves the user input. We then move to the responce view

##### Explain the various modes for the Session state in ASP.NET?**

- InProc: Sessions are stored in the application's processes on a web server
- StateServer: Sessions are stored by utilizing the State Server Windows Administrator service
- SQLServer: a SQL data base is used for to store a sessions information
- Custom:

##### What are the return types from a controller action method **

- View Result
- Redireact result
- Javascript result
- Json result
- Content result

##### How can you maintain sessions in MVC **

- Temp data
- ViewData
- View bag

##### What is REST arcetucture **
REST stands for REpseantail State Transfer. It a collection of constraints for how API's should be designed. There are Six Constarints

1. Uniformed Interface
2. Stateless
3. Cacheable
4. Client-Server
5. Layerd System
6. Code on Demand

##### What is cashing

Cashing allows for the storage of WebPage outputs to reduse over head when providing the most used resourses.

There are three types of cashing for .Net
- Page output Caching
- Page Fragment Caching
- Data Caching


##### What is Kestrel?

Kestrel is a light waight webserver that comes standard with ASP.Net core. It is more light wait than IIS

##### What Is IIS

Internet Information Service is a powerful web server devloped by microsoft. It also can act as a load balancer and can handle simple messaging services. It can also act as a reverse Proxy, taking in a clients request, forwording it to a server and then returning the responce back to the client.

Its main limatation is that it is Windows system dependent.

##### What is a web application framework, and what are its benefits?

A web application framework is a grouping of tools, technologies and practices to help with the building and maintaing of scalable web based applactions. Benafits include:

- Building a dynamic responce that corrisponds to a http request
- Allowing users to log into a system and manage their data
- Storing data in the database
- Handeling database connections
- Routing URL's with appropieate methods
- Supporting sessions
- Formating out puts 

##### Explain how attrabute based routing works

Attrabut based routing works by using decrotive patterns in controler classes to from the routing patter of an API. An example would be for a Blog api. the controle its self would have a [Route("Blog")] attrabute at the top of the controle class to indacate the routing pattern of 'Blog'

Above each method with in the contoler class we would then have the type of Restfull call the method provides + and signafiers or nessesory attrabutes.
[HTTP GET("GetById/{id:Int}")]

This would mean that the Blog/GetById/1234 URL would map to this method.

##### Explain how conventional based routing works

Conventional based routing take more of a hard coded aproch to setting up your mapping. For instance with in the StartUp class you can set up the app.UseEndPoints method and hard code the routing.


##### Explain the consept of middle ware in .Net

Middle ware represents any solution or tool that acts as the plumbing between two systems. An example of this would be the software that collects and handles Incoming and outgoing Http requests. There can be Middle ware of other aspects as well from Communacation, security or database access middle ware acts as the glue between systems.

##### Write and delete a cookie in asp.net

Add
Request.Cookies.Append(Key, Value);

Delete
Request.Cookies.Delete(Key)

##### What’s the HTTPContext object? How can you access it within a Controller?

HTTPContext encapsulates all the information needed for a http request.
You can access this data thought ControllerBase.HttpContext

##### What is the Action class
IActionResult allows us to handle how we respond to a Http Request. We can are able to send back a paylode with a corisponding http stattus code.

Give some examples of responces that can be handled with IActionResult

- ViewResult - generates a new Http View
- RedireactResult - Generates a 302 Http responce that redireact the user to a spesfic URL
- RedireactToRouteResult - Sends a 302 Http responce to point a user to a spesfic URL where that URL is defined using routing
- FileResult - Returns a file
- ContentResult - Returns a provided string or responce
- StatusCodeResult - Sends a raw http responce and code sometimes paired with a body
- NotFoundResponce - returns a 404 message 


##### What is model binding in ASP.NET?

Model binding is a way of defining the patten in which information will be extracted from a incoming Http request. 

As requests can come in differnet forms, from Queries, routes, forms, bodys and headers we need way to indacate to controlers how to extract this information. We user the Attrabutes [FromQuery] and [FromBody] and the like to allow us to extract the information.





