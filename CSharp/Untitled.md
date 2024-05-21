## C# Fundamentals

C# vs .NET

- C# is programming language 
- .NET is framework 

## .NET 

- CLR (Common Language Runtime)
- Class Library

## What is CLR?

so before c# two language of family C/C++ converts code directly into machine code which makes it difficult to run same code on different machines
So C# developers take idea from Java to translate first in intermediate code (bytecode in java) and then translate into machine code accordingly.

C#
 |
IL Code (Intermediate code) - Independent of the computer
|
Native Code(Machine code) - Job of CLR is to convert IL to machine code and the process is called Just-in-time compilation (JIT)


## Architecture of .NET Applications

At very high level App consists of building blocks called classes.

Namespace - Container for related classes.
Assembly(dll or exe)- Container for related namespaces.

```c#
using System;

public class HelloWorld
{
    public static void Main(string[] args)
    {   Console.Write("Hey!");
        Console.WriteLine("Hello Programmer");
        Console.WriteLine("\tBro\nCode");
        Console.ReadKey(); // prevent program from exiting until we press a key
    } 
}
```

```c#

char c = '@';
String name = "DevilXfiero";

Console.WriteLine("Your name is " + c + name);
// typecasting
double a = 3.17;
int b = Convert.ToInt32(a);
Console.WriteLine(b);
Console.WriteLine(b.GetType());
```

## Arrays
```c#
String[] cars = { "BMW", "Mustang", "Mercedes" };

cars[0] = "Tesla";
for(int i=0; i<cars.Length; i++)
{
    Console.WriteLine(cars[i]);
}

foreach (String car in cars)
{
    Console.WriteLine(car);
}
```

## Params keyword

params keyword = a method parameter that takes variable number of arguments.
The parameter type must be a single dimensional array
```c#
double total = Checkout(1.22, 7.89, 88.73);
Console.WriteLine(total);


static double Checkout(params double[] prices)
{
    double total = 0;
    foreach (double price in prices)
    {
        total += price;
    }
    return total;
}
```

Exception - errors that occur during execution.


try - try some code that is considered dangerous.
catch - catches and handles exception when they occur.
finally - always executes regardless of exception catch or not.

## Multidimensional Arrays

```c# 
String[,] parkingLot =
{
    {"a", "b" },
    {"c", "d" },
    {"e", "f" }
};
parkingLot[0, 1] = "k";

for(int i=0; i<parkingLot.GetLength(0); i++)
{
    for(int j=0; j<parkingLot.GetLength(1); j++)
    {
        Console.Write(parkingLot[i, j] + " ");
        
    }
    Console.WriteLine();
}
```


## Method Overriding 

Method overriding provides a new version of method inherited from a parent class inherited method must be abstract, virtual, or already overriden.
Used with ToString(), polymorphism

```c#
Cat cat = new Cat();
Dog dog = new Dog();

cat.Speak();
dog.Speak();
class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("The animal goes *brrr*");
    }
}

class Dog : Animal
{
    public override void Speak()
    {

        Console.WriteLine("The dog goes *woof*");
    }
}

class Cat : Animal
{
    public override void Speak()
    {
        Console.WriteLine("The cat goes *meow*");
    }
}
```

