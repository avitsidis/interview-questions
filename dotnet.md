# .Net

## struct vs class

Do not define a structure unless the type has all of the following characteristics:
– It logically represents a single value, similar to primitive types (integer, double, and so on).
– It has an instance size smaller than 16 bytes.
– It is immutable.
– It will not have to be boxed frequently.

## Covariance, contravariance

In, out uniquement sur des interfaces ou des delegates
Example : Func<in T,out TResult>. 

### Covariance

keyword out, example: Print(IEnumerable<Animals> animals){ } sur lequel on peut passer une liste de chats : Print(cats). Comme Cat < Animal et que IEnumerable est défini comme IEnumerable<out T>.
Covariance > can output > type must be the one defined or its subtype

### Contrvariance

Contravariance > input > we output this type or its ancestors

## iqueryable vs ienumerable

IQueryable -> Database query, Ienumerable Linq Object (in memory)

## linq deferred execution
Query linq executed only if it forced to (ToList, ToArray, …)

## singleton

[MSDN](https://msdn.microsoft.com/en-us/library/ff650316.aspx)

```C#
public sealed class Singleton
{
   private static readonly Singleton instance = new Singleton();

   private Singleton(){}

   public static Singleton Instance
   {
      get
      {
         return instance;
      }
   }
}
```

Static initialization is suitable for most situations. When your application must delay the instantiation, use a non-default constructor or perform other tasks before the instantiation, and work in a multithreaded environment, you need a different solution

```C#
using System;

public sealed class Singleton
{
   private static volatile Singleton instance;
   private static object syncRoot = new Object();

   private Singleton() {}

   public static Singleton Instance
   {
      get 
      {
         if (instance == null) 
         {
            lock (syncRoot) 
            {
               if (instance == null) 
                  instance = new Singleton();
            }
         }

         return instance;
      }
   }
}
```

This approach ensures that only one instance is created and only when the instance is needed. Also, the variable is declared to be volatile to ensure that assignment to the instance variable completes before the instance variable can be accessed. Lastly, this approach uses a syncRoot instance to lock on, rather than locking on the type itself, to avoid deadlocks. 
This double-check locking approach solves the thread concurrency problems while avoiding an exclusive lock in every call to the Instance property method. It also allows you to delay instantiation until the object is first accessed. In practice, an application rarely requires this type of implementation. In most cases, the static initialization approach is sufficient.
Async awaits

## Throw

* throw e;
* throw;
* throw new Exception(“”,e);

## Polymorphism

* Ad-hoc (same method name with different inputs)
* Inheritance (override)
* Duck typing (dynamic object)
* Generic

## Explain the differences between deferred execution and immediate execution in LINQ

## What do the following acronyms stand for: IL, CIL, MSIL, CLI and JIT?

## What are the three types of Generic delegates in the .Net framework?

* Func
* Action
* Predicate

## What is a multicast Delegate?

## What are the differences between keywords const and readonly?

## How events work in C#?

## What is an extension method?

## What does the Nullable<T> type do?

## What are the differences between casting, as keyword and is keyword?

## Garbage Collection

### Links

* [Documentation](https://docs.microsoft.com/en-us/dotnet/standard/garbage-collection/fundamentals)
* [Questions on csharpstar](http://www.csharpstar.com/interview-questions-garbage-collection-csharp/)

## What is Garbage Collection ?

## How the GC knows if an object can be cleaned ?

## Dispose v/s Finalize

## How to manage unmanged resources like files or network connection ?

## Can we enforce garbage collection in .Net ?

## Is there a difference between value type and reference type during garbage collection ?

## What are Generations ?
