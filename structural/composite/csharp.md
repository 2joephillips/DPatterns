---
layout: article
title: State Pattern C# Example
modified:
categories: 
excerpt: 
tags: []
image:
  feature: 
  teaser:
  thumb:
---
<a href="{{ site.url }}/structural/composite" class="btn"> <i class="fa fa-arrow-left" aria-hidden="true"></i> Return to Composite Pattern</a>

![Composite Pattern Structure](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Composite_UML_class_diagram_%28fixed%29.svg/640px-Composite_UML_class_diagram_%28fixed%29.svg.png)

To set-up this example,  ASP.NET core is used create a Console Application. The full <a href="https://github.com/2joephillips/DPatterns-Examples/tree/master/structural/composite/csharp" target="_blank">C Sharp Code Base</a> can be accessed from GitHub.

{% include toc.html %}

## Set-up
This simple console app is used to compile workers with thier rating into teams that have supervisors. With the ability to print out the ratings of each 
worker within the team. In the scenario below we build a team 1 and then add it to another team to show how composite works. Then print all the workers ratings.

```csharp
using System;

namespace CompositeDemo
{
    public class Program
    {
        public static void Main(string[] args)
        {
            //Build Employees 
            Employee jason = new Employee { ID = 1, Name = "Jason Lee Scott", Rating = 3 };
            Employee trini = new Employee { ID = 2, Name = "Trini Kwan", Rating = 4 };
            Employee zach = new Employee { ID = 3, Name = "Zach Taylor", Rating = 5 };
            Employee kimberly = new Employee { ID = 4, Name = "Kimberly Ann Hart", Rating = 3 };
            Employee billy = new Employee { ID = 5, Name = "Billy Cranston", Rating = 4 };
            Employee rose = new Employee { ID = 6, Name = "Tommy Oliver", Rating = 5 };
            
            Employee alpha = new Employee { ID = 7, Name="Alpha 5", Rating = 4};
            Employee zordon = new Employee {ID = 8, Name="Zordon", Rating = 5};

            //Build Team and Set-Supervisor
            Team team1 = new Team { Name= "Team 1", Supervisor = alpha, 
                Workers = {jason, trini, zach, kimberly, billy, rose}};
            
            //Build Team Include Team 1 and alpha as a worker  under this team and Supervisor.
            Team powerTeam = new Team { Name="PowerTeam", Supervisor = zordon, 
                Workers = {alpha, team1}};

            //Print out Power Teams Preformance Summary    
            powerTeam.PerformaceSummary();
        }
    }
}
```


## IEmployee

The IEmployee class is the Component part of the Composite pattern. It declares the interface objects by implementing the default behavior common to all classes.
In this case every instance will have an ID, Name, and the ability to provide a Performace Summary. 

```csharp
namespace CompositeDemo
{
    public interface IEmployee {
        int ID {get;set;}
        string Name {get; set;}
        void PerformaceSummary();
    }
}
```

## Employee

The Employee class is the Leaf representation. In this case an Employee will never have children.

```csharp
using System;

namespace CompositeDemo
{
    public class Employee : IEmployee
    {
        public int ID {get;set;}
        public string Name {get; set;}
        public int Rating{get;set;}
        public void PerformaceSummary(){
            Console.WriteLine("Performance summary of employee: {0} is {1} out 0f 5", Name, Rating);
        }
    }
}
```

## Team

The Team class is the Composite implementation of the IEmployee Class. The team has children and stores child components. In this scenario, it contains a list of IEmployee. This can be a single Employee
or another Team. 

```csharp
using System;
using System.Collections.Generic;

namespace CompositeDemo
{
    public class Team : IEmployee
    {
        public int ID {get;set;}
        public string Name {get; set;}
        public Employee Supervisor {get;set;}
        public List<IEmployee> Workers {get;}

        public Team()
        {
            Name = Name;
            Supervisor = new Employee();
            Workers = new List<IEmployee>();
        }

        public void PerformaceSummary(){
            Console.WriteLine("Team: " + Name);
            Console.WriteLine("Supervisor: " + Supervisor.Name);
            Console.WriteLine("Members Reviews");
            foreach (var worker in Workers)
            {
                worker.PerformaceSummary();
            }
        }
    }
}
```