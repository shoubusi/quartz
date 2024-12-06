---
date created: 2024-08-27
date modified: 2024-10-31
---
# NRules

https://nrules.net/

## Key Concepts

NRules is a powerful rules engine for .NET that allows developers to define and execute business rules in their applications. Here are the key concepts of the NRules library:

1. Rules: These are the core building blocks of NRules. A rule is a class that inherits from the `Rule` base class and defines conditions (When) and actions (Then) using a fluent API.

2. Facts: Facts are the data objects that rules operate on. They can be any .NET object and represent the current state of your system.

3. Rule Session: This is the runtime environment where rules are executed. It manages the working memory (fact repository) and handles rule activation and execution.

4. Pattern Matching: NRules uses the Rete algorithm for efficient pattern matching, allowing it to quickly determine which rules should be activated based on the current set of facts.

5. Working Memory: This is where facts are stored during rule execution. Facts can be inserted, updated, or retracted from the working memory.

6. Agenda: The agenda is a prioritized queue of rule activations that are ready to be executed.

7. Activation: An activation occurs when all conditions of a rule are satisfied by the facts in working memory.

8. Action (Then): The action part of a rule specifies what should happen when the rule is activated and executed.

9. Forward Chaining: NRules uses forward chaining, meaning that rules are executed based on the current state of facts, potentially triggering other rules.

10. Fluent API: NRules provides a fluent API for defining rules, making them easy to read and maintain.

11. Rule Repository: This is where rules are stored and organized. It allows for grouping rules into rulesets for easier management.

12. Linq Expressions: NRules allows the use of LINQ expressions in rule conditions, providing a powerful and familiar way to define complex matching criteria.

Understanding these key concepts is crucial for effectively using the NRules library in your .NET applications.

## Basic Steps

1. Define the facts

Here are some examples of defining facts for NRules:

```csharp
// Example 1: Simple Customer fact
public class Customer
{
    public string Name { get; set; }
    public int Age { get; set; }
    public string Email { get; set; }
}

// Example 2: Order fact with nested Product
public class Order
{
    public int OrderId { get; set; }
    public Customer Customer { get; set; }
    public List<Product> Products { get; set; }
    public decimal TotalAmount { get; set; }
    public DateTime OrderDate { get; set; }
}

public class Product
{
    public string Name { get; set; }
    public decimal Price { get; set; }
    public int Quantity { get; set; }
}

// Example 3: Account fact for financial rules
public class Account
{
    public string AccountNumber { get; set; }
    public decimal Balance { get; set; }
    public AccountType Type { get; set; }
}

public enum AccountType
{
    Checking,
    Savings,
    Investment
}

// Example 4: Inventory fact for stock management
public class InventoryItem
{
    public string SKU { get; set; }
    public string ProductName { get; set; }
    public int QuantityOnHand { get; set; }
    public int ReorderPoint { get; set; }
}

// These fact classes can be used in NRules to define conditions and actions in your business rules.
```

2. Define the rules

```csharp
public class OrderDiscountRule : Rule
{
    public override void Define()
    {
        Order order = null;

        When()
            .Match<Order>(() => order, o => o.Total > 100 && !o.IsEligibleForDiscount);

        Then()
            .Do(ctx => 
            {
                order.IsEligibleForDiscount = true;
                Console.WriteLine($"Order with total ${order.Total} is now eligible for a discount.");
                ctx.Update(order);
            });
    }
}

public class InventoryRestockRule : Rule
{
    public override void Define()
    {
        InventoryItem item = null;

        When()
            .Match<InventoryItem>(() => item, i => i.QuantityOnHand < i.ReorderPoint);

        Then()
            .Do(ctx => Console.WriteLine($"Reorder alert: {item.ProductName} (SKU: {item.SKU}) is below reorder point."));
    }
}

public class AccountBalanceRule : Rule
{
    public override void Define()
    {
        Account account = null;

        When()
            .Match<Account>(() => account, a => a.Type == AccountType.Checking && a.Balance < 100);

        Then()
            .Do(ctx => Console.WriteLine($"Low balance warning for account {account.AccountNumber}"));
    }
}

// Example of using multiple conditions
public class ComplexOrderRule : Rule
{
    public override void Define()
    {
        Order order = null;
        Customer customer = null;

        When()
            .Match<Order>(() => order, o => o.TotalAmount > 1000)
            .And<Customer>(() => customer, c => c.Email != null)
            .And((o, c) => o.Customer.Email == c.Email);

        Then()
            .Do(ctx => 
            {
                Console.WriteLine($"High-value order ({order.OrderId}) placed by {customer.Name}");
                // Additional actions can be performed here
            });
    }
}


```

3. Define the rule repository
4. Compile the rules
5. Create a session
6. Insert facts into the session
7. Fire the rules

## Examples

Give examples for the NRules .NET library

Certainly! I'd be happy to provide some examples for using the NRules .NET library. NRules is a powerful open-source rules engine for .NET that allows you to define business rules in C# and execute them efficiently. Here are a few examples to get you started:

1. Basic Rule Example:

```csharp
public class Customer
{
    public string Name { get; set; }
    public int Age { get; set; }
}

public class DiscountRule : Rule
{
    public override void Define()
    {
        Customer customer = null;

        When()
            .Match<Customer>(() => customer, c => c.Age >= 65);

        Then()
            .Do(ctx => Console.WriteLine($"{customer.Name} is eligible for a senior discount."));
    }
}
```

This rule checks if a customer is 65 or older and prints a message if they're eligible for a senior discount.

2. Using Facts and Asserting:

```csharp
public class Order
{
    public double Total { get; set; }
    public bool IsEligibleForDiscount { get; set; }
}

public class DiscountEligibilityRule : Rule
{
    public override void Define()
    {
        Order order = null;

        When()
            .Match<Order>(() => order, o => o.Total > 100);

        Then()
            .Do(ctx => {
                order.IsEligibleForDiscount = true;
                ctx.Update(order);
            });
    }
}
```

This rule checks if an order total is over 100 and marks it as eligible for a discount if so.

3. Using Multiple Conditions:

```csharp
public class Product
{
    public string Category { get; set; }
    public double Price { get; set; }
}

public class SpecialOfferRule : Rule
{
    public override void Define()
    {
        Product product = null;
        Customer customer = null;

        When()
            .Match<Product>(() => product, p => p.Category == "Electronics" && p.Price > 500)
            .And<Customer>(() => customer, c => c.Age < 30);

        Then()
            .Do(ctx => Console.WriteLine($"Special offer available for {customer.Name} on {product.Category}!"));
    }
}
```

This rule combines conditions on both a product and a customer to determine if a special offer is available.

4. Using Aggregates:

```csharp
public class OrderItem
{
    public string ProductName { get; set; }
    public int Quantity { get; set; }
}

public class LargeOrderRule : Rule
{
    public override void Define()
    {
        IEnumerable<OrderItem> items = null;

        When()
            .Query(() => items, x => x
                .Match<OrderItem>()
                .Collect()
                .Where(c => c.Sum(i => i.Quantity) > 10));

        Then()
            .Do(ctx => Console.WriteLine("Large order detected!"));
    }
}
```

This rule uses an aggregate function to sum the quantities of all order items and triggers when the total quantity exceeds 10.

To use these rules, you would typically:

1. Create an instance of `RuleRepository`
2. Load your rules into the repository
3. Compile the rules
4. Create a session
5. Insert facts (your data objects) into the session
6. Fire the rules

Here's a simple example of how to use the rules:

```csharp
var repository = new RuleRepository();
repository.Load(x => x.From(typeof(DiscountRule).Assembly));

var factory = repository.Compile();

var session = factory.CreateSession();
session.Insert(new Customer { Name = "John Doe", Age = 70 });
session.Fire();
```

These examples should give you a good starting point for working with NRules. Remember to adjust the rules and data models to fit your specific use case.
