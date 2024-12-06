---
date created: 2023-09-28
date modified: 2024-03-15
tags: []
---

# 101-linq-samples

https://learn.microsoft.com/en-us/samples/dotnet/try-samples/101-linq-samples/


`dotnet run --region where-syntax`

## Restrictions

// 1- 5
Restrictions().LowNumbers();
Restrictions().ProductsOutOfStock();
Restrictions().ExpensiveProductsInStock();
Restrictions().DisplayCustomerOrders();

Restrictions().IndexedWhere();
```csharp
var shortDigits = digits.Where((digit, index) => digit.Length < index);
```
?
```
The word five is shorter than its value.
The word six is shorter than its value.
The word seven is shorter than its value.
The word eight is shorter than its value.
The word nine is shorter than its value.
```
<!--SR:!2023-12-21,14,290-->

## Projections

// 6 - 19 (+ 2 for tuples)
Projections().SelectSyntax();
Projections().SelectProperty();
Projections().TransformWithSelect();

Projections().SelectByCaseAnonymous();
```csharp
public int SelectByCaseAnonymous()
{
	#region select-case-anonymous
	string[] words = { "aPPLE", "BlUeBeRrY", "cHeRry" };

	var upperLowerWords = from w in words
						  select new { Upper = w.ToUpper(), Lower = w.ToLower() };

	foreach (var ul in upperLowerWords)
	{
		Console.WriteLine($"Uppercase: {ul.Upper}, Lowercase: {ul.Lower}");
	}
	#endregion
	return 0;
}
```
?
```
Uppercase: APPLE, Lowercase: apple
Uppercase: BLUEBERRY, Lowercase: blueberry
Uppercase: CHERRY, Lowercase: cherry
```
<!--SR:!2023-12-17,10,270-->

Projections().SelectByCaseTuple();
```csharp
public int SelectByCaseTuple()
{
	#region select-case-tuple
	string[] words = { "aPPLE", "BlUeBeRrY", "cHeRry" };

	var upperLowerWords = from w in words
						  select (Upper : w.ToUpper(), Lower : w.ToLower());

	foreach (var ul in upperLowerWords)
	{
		Console.WriteLine($"Uppercase: {ul.Upper}, Lowercase: {ul.Lower}");
	}
	#endregion
	return 0;
}
```
?
```
Uppercase: APPLE, Lowercase: apple
Uppercase: BLUEBERRY, Lowercase: blueberry
Uppercase: CHERRY, Lowercase: cherry
```
<!--SR:!2023-12-16,9,270-->

Projections().SelectAnonymousConstructions();
```csharp
public int SelectAnonymousConstructions()
{
	#region select-new-type
	int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };
	string[] strings = { "zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine" };

	var digitOddEvens = from n in numbers
						select new { Digit = strings[n], Even = (n % 2 == 0) };

	foreach (var d in digitOddEvens)
	{
		Console.WriteLine($"The digit {d.Digit} is {(d.Even ? "even" : "odd")}.");
	}
	#endregion
	return 0;
}
```
?
```
The digit five is odd.
The digit four is even.
The digit one is odd.
The digit three is odd.
The digit nine is odd.
The digit eight is even.
The digit six is even.
The digit seven is odd.
The digit two is even.
The digit zero is even.
```
<!--SR:!2023-12-17,10,274-->

Projections().SelectTupleConstructions();

Projections().SelectPropertySubset();
```csharp
public int SelectPropertySubset()
{
	//todo
	#region select-subset-properties
	List<Product> products = GetProductList();

	var productInfos = from p in products
					   select (p.ProductName, p.Category, Price : p.UnitPrice);

	Console.WriteLine("Product Info:");
	foreach (var productInfo in productInfos)
	{
		Console.WriteLine($"{productInfo.ProductName} is in the category {productInfo.Category} and costs {productInfo.Price} per unit.");
	}
	#endregion
	return 0;
}
```
?
```
Product Info:
Chai is in the category Beverages and costs 18.0000 per unit.
Chang is in the category Beverages and costs 19.0000 per unit.
Aniseed Syrup is in the category Condiments and costs 10.0000 per unit.
...
```
<!--SR:!2023-12-18,4,279-->

Projections().SelectWithIndex();
```csharp
public int SelectWithIndex()
{
    #region select-with-index
    int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };

    var numsInPlace = numbers.Select((num, index) => (Num : num, InPlace : (num == index)));

    Console.WriteLine("Number: In-place?");
    foreach (var n in numsInPlace)
    {
        Console.WriteLine($"{n.Num}: {n.InPlace}");
    }
    #endregion
    return 0;
}
```
?
```
5: False
4: False
1: False
3: True
9: False
8: False
6: True
7: True
2: False
0: False
```
<!--SR:!2023-12-17,3,263-->

Projections().SelectWithWhere();

Projections().SelectFromMultipleSequences();
```csharp
public int SelectFromMultipleSequences()
{
	#region select-many-syntax
	int[] numbersA = { 0, 2, 4, 5, 6, 8, 9 };
	int[] numbersB = { 1, 3, 5, 7, 8 };

	var pairs = from a in numbersA
				from b in numbersB
				where a < b
				select (a, b);

	Console.WriteLine("Pairs where a < b:");
	foreach (var pair in pairs)
	{
		Console.WriteLine($"{pair.a} is less than {pair.b}");
	}
	#endregion
	return 0;
}
```
?
```
Pairs where a < b:
0 is less than 1
0 is less than 3
0 is less than 5
0 is less than 7
0 is less than 8
2 is less than 3
2 is less than 5
2 is less than 7
2 is less than 8
4 is less than 5
4 is less than 7
4 is less than 8
5 is less than 7
5 is less than 8
6 is less than 7
6 is less than 8
```
<!--SR:!2023-12-18,4,279-->

Projections().SelectFromChildSequence();
```csharp
public int SelectFromChildSequence()
{            
	#region select-many-drilldown
	List<Customer> customers = GetCustomerList();

	var orders = from c in customers
				 from o in c.Orders
				 where o.Total < 500.00M
				 select (c.CustomerID, o.OrderID, o.Total);

	foreach(var order in orders)
	{
		Console.WriteLine($"Customer: {order.CustomerID}, Order: {order.OrderID}, Total value: {order.Total}");
	}
	#endregion
	return 1;
}
```
?
```
Customer: ALFKI, Order: 10702, Total value: 330.00
Customer: ALFKI, Order: 10952, Total value: 471.20
Customer: ANATR, Order: 10308, Total value: 88.80
Customer: ANATR, Order: 10625, Total value: 479.75
Customer: ANATR, Order: 10759, Total value: 320.00
```
<!--SR:!2023-12-18,4,279-->

Projections().SelectManyWithWhere();
Projections().SelectManyWhereAssignment();
Projections().SelectMultipleWhereClauses();

//todo

Projections().IndexedSelectMany();

## Partitions

// 20 - 27
Partitions().TakeSyntax();
Partitions().NestedTake();
Partitions().SkipSyntax();
Partitions().NestedSkip();
Partitions().TakeWhileSyntax();
Partitions().IndexedTakeWhile();
Partitions().SkipWhileSyntax();
Partitions().IndexedSkipWhile();

## Orderings

// Ordering: 28-39
Orderings().OrderbySyntax();
Orderings().OrderbyProperty();
Orderings().OrderByProducts();
Orderings().OrderByWithCustomComparer();
Orderings().OrderByDescendingSyntax();
Orderings().OrderProductsDescending();
Orderings().DescendingCustomComparer();
Orderings().ThenBySyntax();
Orderings().ThenByCustom();
Orderings().ThenByDifferentOrdering();
Orderings().CustomThenByDescending();
Orderings().OrderingReversal();

## Groupings

// Grouping: 40 - 45
Groupings().GroupingSyntax();
Groupings().GroupByProperty();
Groupings().GroupByCategory();
Groupings().NestedGrouBy();
Groupings().GroupByCustomComparer();
Groupings().NestedGroupByCustom();

## SetOperations

// Set operations: 46 - 53
SetOperations().DistinctSyntax();
SetOperations().DistinctPropertyValues();
SetOperations().UnionSyntax();
SetOperations().UnionOfQueryResults();
SetOperations().IntersectSynxtax();
SetOperations().IntersectQueryResults();
SetOperations().DifferenceOfSets();
SetOperations().DifferenceOfQueries();

## Conversions

// Conversion Operators: 54 - 57
Conversions().ConvertToArray();
Conversions().ConvertToList();
Conversions().ConvertToDictionary();
Conversions().ConvertSelectedItems();

## ElementOperations

// Element operators: 58-64 (60 is missing.)
ElementOperations().FirstElement();
ElementOperations().FirstMatchingElement();
ElementOperations().MaybeFirstElement();
ElementOperations().MaybeFirstMatchingElement();
ElementOperations().ElementAtPosition();

## Generators

// Generator operators: 65,66
Generators().RangeOfIntegers();
Generators().RepeatNumber();

## Quantifiers

// Quantifiers: 67 - 72 (68 and 71 are missing)
Quantifiers().AnyMatchingElements();
Quantifiers().GroupedAnyMatchedElements();
Quantifiers().AllMatchedElements();
Quantifiers().GroupedAllMatchedElements();

## AggregateOperators

// Aggregators: 73 - 93 (75 is missing)
AggregateOperators().CountSyntax();
AggregateOperators().CountConditional();
AggregateOperators().NestedCount();
AggregateOperators().GroupedCount();
AggregateOperators().SumSyntax();
AggregateOperators().SumProjection();
AggregateOperators().SumGrouped();
AggregateOperators().MinSyntax();
AggregateOperators().MinProjection();
AggregateOperators().MinGrouped();
AggregateOperators().MinEachGroup();
AggregateOperators().MaxSyntax();
AggregateOperators().MaxProjection();
AggregateOperators().MaxGrouped();
AggregateOperators().MaxEachGroup();
AggregateOperators().AverageSyntax();
AggregateOperators().AverageProjection();
AggregateOperators().AverageGrouped();
AggregateOperators().AggregateSyntax();

## SequenceOperations

// Miscellaneous:
SequenceOperations().ConcatSeries();
SequenceOperations().ConcatProjection();
SequenceOperations().EqualSequence();
SequenceOperations().Linq97();

## QueryExecution

QueryExecution().DeferredExecution();
QueryExecution().EagerExecution();
QueryExecution().ReuseQueryDefinition();

## JoinOperations

JoinOperations().CrossJoinQuery();
JoinOperations().GroupJoinQquery();
JoinOperations().CrossGroupJoin();
JoinOperations().LeftOuterJoin();
