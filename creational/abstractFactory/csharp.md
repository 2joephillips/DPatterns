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
For this example there are two types of pizza Chicago and New York style.

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