# Decorator Pattern in C#

## Overview
The Decorator Pattern is a structural design pattern used to dynamically add behavior to individual objects without affecting the behavior of other objects from the same class. This pattern is particularly useful in C# for extending functionality in a flexible and reusable manner.

## Why Use the Decorator Pattern?
- **Enhances functionality**: Allows for adding new behavior to objects without altering their structure.
- **Promotes code reusability**: Encourages smaller, reusable classes instead of monolithic ones.
- **Increases flexibility**: More flexible than inheritance for extending functionality.

## Implementation

### Step 1: Define the Component Interface
This interface represents the original object that can be dynamically extended.

```csharp
public interface ICoffee
{
    string GetDescription();
    double GetCost();
}
```

### Step 2: Create Concrete Components
Implement the interface with concrete classes. These are objects that can be decorated.

```csharp
public class BasicCoffee : ICoffee
{
    public string GetDescription() => "Basic Coffee";

    public double GetCost() => 2.0;
}
```

### Step 3: Create the Base Decorator
This abstract class implements the component interface and has a reference to a component object.

```csharp
public abstract class CoffeeDecorator : ICoffee
{
    protected ICoffee _coffee;

    public CoffeeDecorator(ICoffee coffee)
    {
        _coffee = coffee;
    }

    public virtual string GetDescription() => _coffee.GetDescription();

    public virtual double GetCost() => _coffee.GetCost();
}
```

### Step 4: Create Concrete Decorators
Extend the functionality of objects by creating concrete decorators.

```csharp
public class MilkDecorator : CoffeeDecorator
{
    public MilkDecorator(ICoffee coffee) : base(coffee) { }

    public override string GetDescription() => $"{_coffee.GetDescription()}, with milk";

    public override double GetCost() => _coffee.GetCost() + 0.5;
}

public class SugarDecorator : CoffeeDecorator
{
    public SugarDecorator(ICoffee coffee) : base(coffee) { }

    public override string GetDescription() => $"{_coffee.GetDescription()}, with sugar";

    public override double GetCost() => _coffee.GetCost() + 0.25;
}
```

## Example Usage

```csharp
class Program
{
    static void Main(string[] args)
    {
        ICoffee basicCoffee = new BasicCoffee();
        Console.WriteLine($"{basicCoffee.GetDescription()} Cost: ${basicCoffee.GetCost()}");

        ICoffee milkCoffee = new MilkDecorator(basicCoffee);
        Console.WriteLine($"{milkCoffee.GetDescription()} Cost: ${milkCoffee.GetCost()}");

        ICoffee sweetCoffee = new SugarDecorator(milkCoffee);
        Console.WriteLine($"{sweetCoffee.GetDescription()} Cost: ${sweetCoffee.GetCost()}");
    }
}
```

## Conclusion
The Decorator Pattern in C# offers a flexible approach to adding new functionalities to objects. It's a powerful tool for creating scalable and maintainable code, especially in systems where extending capabilities at runtime is essential.
