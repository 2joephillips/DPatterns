---
layout: article
title: Abstract Factory Pattern C# Example
modified:
categories: 
excerpt: 
tags: []
image:
  feature: 
  teaser:
  thumb:
---

<a href="{{ site.url }}/creational/abstractFactory" class="btn"> <i class="fa fa-arrow-left" aria-hidden="true"></i> Return to Abstract Factory Pattern</a>

![State Pattern Structure](http://www.dofactory.com/images/diagrams/net/abstract.gif)

To set-up this example,  ASP.NET core is used create a Console Application. The full <a href="https://github.com/2joephillips/DPatterns-Examples/tree/master/creational/abstractFactory/csharp" target="_blank">C Sharp Code Base</a> can be accessed from GitHub.

{% include toc.html %}

## Set-up
Within this application, <code>Main()</code>, is used to print out several commands and new up the type of 
pizza, provide a list of pizzas that each type has, and places an order for a specific type of pizza.  
For this example there are two types of pizza Chicago and New York style. These types are our Concrete Factories for our Abstract Factory IPizzaStore.
Each Concrete Factory is able to create a concrete Product/pizza from our IPizza Abstract Product class.

To help in organization I have used two folders to organize the code. Our Interfaces used for abstraction are within an Contracts folder giving it the namespace
AbstractFactoryPattern.Contracts, and the concrete classes are in AbstractFactoryPattern.Services.

```csharp
using System;
using AbstractFactoryPattern.Contracts;
using AbstractFactoryPattern.Services;

namespace AbstractFactoryPattern
{
    public class Program
    {
        public static void Main(string[] args)
        {
            Console.WriteLine("Welcome." + Environment.NewLine);
            IPizzaStore store = new ChicagoStylePizza();
            
            store.listPizzas();

            System.Console.WriteLine("What type of Chicago Style pizzas' do you have?"+ Environment.NewLine);

            Console.WriteLine("Can I order Deep Dish Pizza."+ Environment.NewLine);  
            IPizza pizza = store.orderPizza("Deep Dish");
            pizza.createPizza();
            
            Console.WriteLine(Environment.NewLine);
            Console.WriteLine(Environment.NewLine);

            Console.WriteLine("Welcome."+ Environment.NewLine);
            IPizzaStore store1 = new NewYorkStylePizza();
            
            store.listPizzas();

            System.Console.WriteLine("What type of New York Style pizzas' do you have?"+ Environment.NewLine);
            
            Console.WriteLine("Can I order Deep Hand Tossed."+ Environment.NewLine);
            IPizza pizza2 = store.orderPizza("HandTossed");
            pizza.createPizza();
        }
    }
}
```

## Abstract Factory
* **Abstract Factory** declares an interface for operations that create abstract products.

```csharp
namespace AbstractFactoryPattern.Contracts {
    interface IPizzaStore{
        void listPizzas();
        IPizza orderPizza(string type);
    }
}
```

## Concrete Factory
* **Concrete Factory** implements the operations to create concrete product objects.

### Chicago Style
```csharp
public class ChicagoStylePizza : IPizzaStore
    {
        List<String> Pizzas = new List<String>() {"Deep Dish Pizza", "Stuffed Pizza"};
        public IPizza orderPizza(string type)
        {
            if(type == "Deep Dish"){
                return new DeepDishPizza();
            }
            else {
                return new StuffedPizza();
            }
        }

        public void listPizzas()
        {
            Console.WriteLine("The following Chicago Style Pizzas are available");
            foreach(string pizza in Pizzas){
                Console.WriteLine(pizza);
            }
            Console.WriteLine(Environment.NewLine);
        }
    }
```
### New York Style
```csharp
 public class NewYorkStylePizza : IPizzaStore
    {
        List<String> Pizzas = new List<String>() {"Hand-tossed Pizza", "Thin-crust Pizza"};
        public IPizza orderPizza(string type)
        {
            if(type == "HandTossed"){
                return new HandTossedPizza();
            }
            else {
                return new ThinCrustPizza();
            }
        }

        public void listPizzas()
        {
            Console.WriteLine("The following Chicago Style Pizzas are available" );
            foreach(string pizza in Pizzas){
                Console.WriteLine(pizza);
            }
            Console.WriteLine(Environment.NewLine);
        }
    }
```

## Abstract Product
* **Abstract Product** declares an interface for a type of product.

```csharp
namespace AbstractFactoryPattern.Contracts {
    public interface IPizza{
        void createPizza();
    }
}
```

## Product
* **Product** defines a product object to be created by the corresponding concrete factory and implements the Abstract Product interface.

### Chicago Style Pizzas
```csharp
    public class DeepDishPizza : IPizza{
        public void createPizza(){
            Console.WriteLine("Deep Dish Pizza");
        }
    }
```

```csharp
    public class StuffedPizza : IPizza{
        public void createPizza(){
            Console.WriteLine("Stuffed Pizza");
        }
    }
```

### New York Style Pizzas
```csharp
    public class HandTossedPizza : IPizza{
        public void createPizza(){
            Console.WriteLine("Hand-tossed Pizza");
        }
    }
```

```csharp
    public class ThinCrustPizza : IPizza{
        public void createPizza(){
            Console.WriteLine("Thin-crust Pizza");
        }
    }
```