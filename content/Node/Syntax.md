## Syntax

### Variables

```csharp
<modifier> <datatype> <variablename> = <initialvalue>;
```

### Enum Types

```csharp
enum Color
{
    Red,
    Green,
    Blue
}
```

### Structure Types

```csharp
struct Point
{
    public int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

### Tuple Types

```csharp
(double, int) t1 = (4.5, 3);
Console.WriteLine($"Tuple with elements {t1.Item1} and {t1.Item2}."); // Output => Tuple with elements 4.5 and 3.

(double Sum, int Count) t2 = (4.5, 3);
Console.WriteLine($"Sum of {t2.Count} elements is {t2.Sum}."); // Output => Sum of 3 elements is 4.5.
```

### Delegate Types

```csharp
public delegate int PerformCalculation(int x, int y);
```

### Interface Types

```csharp
public interface IShape
{
  void Draw();
}
class Circle : IShape
{
    public void Draw()
    {
      Console.WriteLine("Circle Draw");
    }
}
static void Main(string[] args)
{
    IShape c = new Circle();
    c.Draw(); // Outputs "Circle Draw"
}
```

### Array Types


### Classes


