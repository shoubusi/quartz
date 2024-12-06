---
tags: knowledge
archived: false
---
# Delegates and lambdas

## summary

The provided web resource from Microsoft's documentation explains the concepts of delegates and lambdas in the .NET framework. Here's a summary of the key points:

1. **Delegates**: A delegate in .NET is a type that represents references to methods with a specific parameter list and return type. Methods matching this signature can be assigned to a delegate variable and called directly or passed as arguments to other methods.

2. **Example of Delegate Use**: The document provides an example where a delegate named `Reverse` is defined to reverse a string. A method `ReverseString` is then implemented to match this delegate and is assigned to a delegate variable `rev`, which is used to invoke the method.

3. **Built-in Delegate Types**: .NET includes built-in delegate types such as `Func<>`, `Action<>`, and `Predicate<>` for common scenarios:
   - `Action<>`: Used for methods that perform an action without returning a value.
   - `Func<>`: Used for methods that transform input arguments into a specified result.
   - `Predicate<>`: Used to determine if an argument satisfies a condition, essentially a `Func<T, bool>`.

4. **Anonymous Delegates**: Introduced in .NET Framework 2.0, anonymous delegates allow the creation of "inline" delegates without specifying an additional type or method. An example is given where an anonymous delegate is used to filter a list of numbers to find even numbers.

5. **Lambda Expressions**: Introduced in C# 3.0, lambda expressions are a syntactic convenience for delegates. They allow for the declaration of parameters and a method body without a formal identity. Lambdas can be directly used in event handlers or LINQ queries. The document provides an example of using a lambda expression to filter a list of numbers for even values.

6. **Lambdas as Delegates**: Lambda expressions are essentially delegates and can be used interchangeably in scenarios such as event handling.

7. **Further Reading and Resources**: The document suggests further reading on delegates and lambda expressions and mentions the transition from GitHub Issues to a new feedback system for content feedback in 2024.

8. **Community Contribution**: The content source is on GitHub, where the community can contribute by creating and reviewing issues and pull requests.

This summary encapsulates the main ideas presented in the Microsoft documentation on delegates and lambdas in .NET.

## examples

.NET includes built-in delegate types such as `Func<>`, `Action<>`, and `Predicate<>` for common scenarios:
   - `Action<>`: Used for methods that perform an action without returning a value.
   - `Func<>`: Used for methods that transform input arguments into a specified result.
   - `Predicate<>`: Used to determine if an argument satisfies a condition, essentially a `Func<T, bool>`.

```csharp
// Action<>: Used for methods that perform an action without returning a value.

public delegate void MyAction(string message);

public void PrintMessage(string message)
{
    Console.WriteLine(message);
}

// Create an instance of the delegate and assign it to a method
MyAction myAction = PrintMessage;

// Invoke the delegate
myAction("Hello from Action delegate!");

// Func<>: Used for methods that transform input arguments into a specified result.

public delegate int MyFunc(int x, int y);

public int AddNumbers(int x, int y)
{
    return x + y;
}

// Create an instance of the delegate and assign it to a method
MyFunc myFunc = AddNumbers;

// Invoke the delegate and get the result
int result = myFunc(5, 3);

Console.WriteLine($"Result of addition: {result}");

// Predicate<>: Used to determine if an argument satisfies a condition.

public delegate bool MyPredicate(int number);

public bool IsEven(int number)
{
    return number % 2 == 0;
}

// Create an instance of the delegate and assign it to a method
MyPredicate myPredicate = IsEven;

// Invoke the delegate and get the result (true or false)
bool isEven = myPredicate(4);

Console.WriteLine($"Is 4 even? {isEven}"); 
```

**Explanation:**

* **Delegates:**  Delegates act as pointers to methods. They allow you to pass methods as arguments to other methods or store them in variables.

* **`Action<>`:** The `MyAction` delegate takes a `string` message and prints it to the console. 
* **`Func<>`:** The `MyFunc` delegate takes two integers (`x`, `y`) and returns their sum.
* **`Predicate<>`:** The `MyPredicate` delegate takes an integer and returns `true` if it's even, `false` otherwise.

**Key Points:**

* Delegates provide a powerful way to work with methods in a flexible and dynamic manner.
* You can create your own custom delegates or use the built-in ones like `Action`, `Func`, and `Predicate`.
* The generic type parameters (`<T>`, `<T1, T2>`, etc.) in these delegates specify the types of arguments the methods they point to accept and the type of result they return.

---

give examples to explain .NET includes built-in delegate type `Func<>`, and it's generic type parameters

## Delegates and Lambdas in .NET

Delegates in .NET are essentially function pointers. They represent methods and allow you to pass them around as arguments or return them from other methods. This promotes code reusability and modularity.

###  `Func<>` Delegate

The `Func<>` delegate is a powerful tool that allows you to represent generic functions. Its generic type parameters define the input types and the output type of the function it represents. 

Here's a breakdown with examples:

**Syntax:**

```csharp
Func<T1, T2, ..., TR>
```

Where:

* `T1`, `T2`, ..., `TR` represent the input types (parameters) of the function.
* `Func` indicates that it's a delegate representing a function.

**Examples:**

1. **Adding two integers:**

```csharp
Func<int, int, int> add = (x, y) => x + y;

int result = add(5, 3); // result will be 8
```

In this example, `add` is a `Func` delegate that takes two integers as input and returns their sum.

2. **Multiplying two doubles:**

```csharp
Func<double, double, double> multiply = (a, b) => a * b;

double product = multiply(2.5, 4); // product will be 10
```

Here, `multiply` is a `Func` delegate that multiplies two doubles.

3. **Returning a string based on an integer:**

```csharp
Func<int, string> getGreeting = (number) => {
  if (number == 0) {
    return "Hello!";
  } else {
    return "Welcome!";
  }
};

string greeting = getGreeting(1); // greeting will be "Welcome!"
```

This example demonstrates a `Func` delegate that takes an integer and returns a different string based on its value.

**Key Points:**

* `Func<>` delegates are powerful for representing generic functions.
* You can pass them as arguments to other methods or return them from methods.
* Lambdas provide a concise syntax for defining anonymous functions, often used with `Func<>` delegates.
