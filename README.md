interview
=========

Classic questions for interviews

## .NET Architecture

- What is the [**CLR**] Common Language Runtime?
It provide an environment to run all .NET programas (**ILCode**), the code which runs under the CLR is called as **Managed Code**

- What are the [**BCL**] Base Class Library/ [**FCL**] .NET Framework Class Library?
The Class Library can be seen as libraries provided by .NET in order to ease programing

- What is [**CTS**] Common Type System?
It describes set of data type that can be used in different .NET languages in common, **CTS** ensures that objects written in different .NET languages can interact with each other.

- What is [**CLS**] Common Language Specifications?
It is a sub set of CTS and it specifies a set of rules that needs to be adhered or satified by all language compilers targeting **CRL**. It helps it cross language inheritance and class language debuging.

- What is [**JIT**] Just In Time compiler?
The **CLR** invokes **JIT** compiler which compile the ILCode to native executable code (exe or dll=Dynamic Link Library)

- What is **Intermediate Language** [MSIL, CIL, IL]?
Is an Intermediate code called **IL**, understable by **CLR**, IL is an OS and H/W independent Code.

## Object Oriented Programming

- What is a **Class**?
A Class is an encapsulation of properties and methods that are used to represent a real-time entity. It is a data structure that brings all the instances together in a single unit.

- What is an **Object**?
An Object in an instance of a Class. Technically, it is just a block of memory allocated that can be stored in the form of Variables, Array or a Collection.

- What are the **fundamental OOP concepts**?

**Encapsulation** – The Internal representation of an object is hidden from the view outside object’s definition. Only the required information can be accessed whereas the rest of the data implementation is hidden.

**Abstraction** – It is a process of identifying the critical behavior and data of an object and eliminating the irrelevant details.

**Inheritance** – It is the ability to create new classes from another class. It is done by accessing, modifying and extending the behavior of objects in the parent class.

**Polymorphism** – The name means, one name, many forms. It is achieved by having multiple methods with the same name but different implementations.

- What is an **Interface**?
An Interface is a class with no implementation. The only thing that it contains is the declaration of methods, properties, and events.

- What are the **different types of classes in C#**?

**Partial class** – Allows its members to be `divided or shared with multiple .cs files`. It is denoted by the keyword Partial.

**Sealed class** – It is a class which `cannot be inherited`. To access the members of a sealed class, we need to create the object of the class.  It is denoted by the keyword Sealed.

**Abstract class** – It is a class whose object `cannot be instantiated. The class can only be inherited`. It should contain at least one method.  It is denoted by the keyword abstract.

`
abstract class AbsMath
{
  public abstract int Sum(int X, int Y);
  public virtual int Subtract(int X, int Y)
  {
    return X - Y;
  }
}
public class impMath : AbsMath
{
  override public int Sum(int X, int Y)
  {
    return X + Y;
  }
  // Optional
  override public int Subtract(int X, int Y)
  {
    // use to extend
    base.Subtract(X, Y);
    //...
  }
}
`

**Static class** – It is a class which `does not allow inheritance`. The members of the class are also static.  It is denoted by the keyword static. This keyword tells the compiler to check for any accidental instances of the static class.

- What are teh difference between a Class and Struct?

**Class**
Support Inheritance
Class is Pass by reference (**reference type**)
Member are private by default
Good for larger complex objects
Can use waste collector for memory management

**Struct**
Does not support Inheritance
Struct is Pass by Copy (**Value Type**)
Members are public by default
Good for Small insolated models
Cannot use Garbage Collector and hence no Memory Management

- What are the difference _between_ **Virtual method** and **Abstract method**?

A **Virtual Method** must always _have a default implementation_. However, it can be overriden in the derived class, though not mandatory. It can be overriden using override keyword.

An **Abstract method** **does not have an implementation**. It resides in the abstract class. It is mandatory that the derived class implements the abstract method. An override keyword is not necessary here though it can be used

- How is Exception Handling implemented in C#?

Exception handling is done using four keywords in C#:

**try** – Contains a block of code for which an exception will be checked.
**catch** – It is a program that catches an exception with the help of exception handler.
**finally** – It is a block of code written to execute regardless whether an exception is caught or not.
**Throw** – Throws an exception when a problem occurs.

- What are **C# I/O Classes**? What are the commonly used I/O Classes?
C# has **System.IO** namespace, consisting of classes that are used to perform various operations on files like creating, deleting, opening, closing etc.

- Which are the commonly used I/O classes?

**File** - Helps in manipulating a file

**StreamWriter** - Used for writing characters to a stream

`StreamWriter sw = new StreamWriter(“C:\ReadMe.txt”);`

**StreamRead** - Used for reading characters to a stream

`StreamReader sr = new StreamReader(“C:\ReadMe.txt”);`

**StringWriter** - Used for reading a string buffer.

**StringReader** - Used for writing a string buffer.

**Path** - Used for performing operations related to path information.

- What is a **Destructor** in C#?
A Destructor **is used to clean up the memory and free the resources**. But in C# this **is done by the Garbage Collector** on its own. **System.GC.Collect() is called internally for cleaning up**. But somethimes it may be necessary to implment destructor manually
`~Car()
{
  Console.Writeline("destruction");
}`

- What are **Boxing and Unboxing**?
Converting a **Value to reference type is called Boxing**

`int intValue = 10;
object boxedValue = intValue;`

Explicit conversion of same **reference type back to value type is called unboxing**

`int UnBoxing = int(boxedValue)`

- What are the difference between **continue** and **break** statements?

**break** statement breaks the look, It makes the control of the program to exit the loop.

**continue** it break the current look and move to the next iteration.

- What is Jagged Array?

A Jagged array is an array whose elements are arrays. It also called as the array of arrays. It can be either single or multiple dimensions.

`int[] jaggedArray = new int[4][];`

- What are **Regular Expression**?
Is a **pattern** that could be matched against an input text
`string strValues = "4 AND 5";
Match match = Regex.Match(value, @"\d");
if (match.Success)
{
  Console.WriteLine(match.Value);
}
// move to the next value
match = match.NextMatch();
if (match.Success)
{
  Console.WriteLine(match.Value);
}
`

- What are **Delegate**?
A Delegate **is a variable that holds the reference to a method**. Hence it is a function pointer of reference type. All Delegates are derived from **System.Delegate** namespace. Both and the method that it refers to can have the same signature.
`delegate int NumberChanger(int n);
class TestDelegate {
  static int num = 10;
      
  public static int AddNum(int p) {
     num += p;
     return num;
  }
  public static int MultNum(int q) {
     num *= q;
     return num;
  }
  public static int getNum() {
     return num;
  }
  static void Main(string[] args) {
     //create delegate instances
     NumberChanger nc1 = new NumberChanger(AddNum);
     NumberChanger nc2 = new NumberChanger(MultNum);

     //calling the methods using the delegate objects
     nc1(25);
     Console.WriteLine("Value of Num: {0}", getNum());
     nc2(5);
     Console.WriteLine("Value of Num: {0}", getNum());
     Console.ReadKey();
  }
}
`

- What are **Events**?
Events **are user actions that generate notifications to the application to which it must respond**. The user actions can be mouse movements, keypress and so on.
`class Program
{
  public delegate string MyDel(string str);
  event MyDel MyEvent;

  public string WelcomeUser(string username)
  {
      return "Welcome " + username;
  }

  // constructor
  public Program()
  {
      this.MyEvent += new MyDel(this.WelcomeUser);
  }

  // entry point
  static void Main(string[] args)
  {
      Program obj1 = new Program();
      string result = obj1.MyEvent("Sergio");
      Console.WriteLine(result);
      Console.Read();
  }
}`

- What are **Generic Class**?
Generics or Generic class is used to create classes or object which do not have any specific data type.
`class Program
{
  public void Compare(int a, int b) { }
  public void Compare(string a, string b) { }
  class CompareGenericClass<T>
  {
    public void compare(T x, T y)
    {
    }
  }
  static void Main(string[] args)
  {
    CompareGenericClass<string> stringCompare = new CompareGenericClass<string>();
    stringCompare.Compare("","");
    
    CompareGenericClass<int> intCompare = new CompareGenericClass<int>();
    intCompare.Compare(2,3);
  }
}
`

- What is **Thread**? and What is **Multithreading**?
**Thread** is a set of instructions that can be executed, which will enable our program to perform concurrent processing. Concurrent processing helps us do more than one operation at a time. By default, C# has only one thread. But the other threads can be created to execute the core in parallel with the original thread.

**Thread as a live cycle** It **start** whenever a thread class is created and is terminated after the execution. **System.Threading** is the namespace which needs to be included to create threads and use its members.

Threads are create by extending the Thread class. **Start()** methods is used to begin thread execution.

`ThreadStart methodThread = new ThreadStart(callthread);
Thread childThread = new Thread(methodThread);
childTread.Start();
`

- What are **Async and Await?**
Async and Await keywords are used to create asynchronous methods in C#.
`public async Task<int> CalculateCount()
{
  await Task.Delay(1000);
  return 1;
}
public async Task myMethod()
{
  Task<int> count = CalculateCount();
  int result = await count;
}
`

- What are the **difference between Task and Thread**?

**A task is something you want done**.

**A thread is one of the many possible workers which performs that task**.

In .NET 4.0 terms, a **Task represents an asynchronous operation**. **Thread(s) are used to complete that operation** by breaking the work up into chunks and assigning to separate threads.

- Explain **Lock**, **Monitors**, and **Mutex** Object in threading?
**Lock** keyword ensures that only one thread can enter a particular section of code at any given time.
`lock(ObjA) means the lock is placed on ObjA until this process releases it, no other thread can access ObjA`

**Mutex** is also **like a lock but it can work across multiple processess at a time**. **WaitOne() is used to lock and ReleaseMutex() is used to release the lock**. But Mutex is slower than lock as it takes time to acquire and release it.

- What is **Race Condition**?

A **Race Condition** occurs when two threads access the same resource and are trying to change it at the same time. The thread which will be able to access the resource first cannot be predicted.

If we have two threads, T1 and T2 they are trying to access a share resource called X. and if both the threads try to write a value to X, the last value written to X will be saved.

- What is a **Thread Pooling**? **System.Threading.ThreadPool**

A thread pool is a collection on threads. These threads can be used to perform tasks without disturbing the primary thread. Once the thread completes the task, the thread returns to the pool.

- What is **Serialization**?

**Serialization** is a **process of converting a object to its binary format**. Once it is **converted to bytes**, it can be easily stored and written to a disk or any such storage devices. Serializations are mainly useful when we do not want to lose the original form of the code and it can be retrieved anytime in the future.

**Deserialization** is the reverse process.
