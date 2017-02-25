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

<a href="{{ site.url }}/behavioral/state" class="btn"> <i class="fa fa-arrow-left" aria-hidden="true"></i> Return to State Pattern</a>

![State Pattern Structure](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e8/State_Design_Pattern_UML_Class_Diagram.svg/470px-State_Design_Pattern_UML_Class_Diagram.svg.png)

To set-up this example,  ASP.NET core is used create a Console Application. The full <a href="https://github.com/2joephillips/DPatterns-Examples/tree/master/behavioral/state/csharp" target="_blank">C Sharp Code Base</a> can be accessed from GitHub.

{% include toc.html %}

## Set-up
Within the Client section, <code>Main()</code>, we new up the TrafficLight. 
Plus, we start the light with a call to <code>Activate()</code> that sets the light to running.
To stop the application from running forever, we wrap the calls within a loop so that we can stop it by pressing "ESC".
The <code> Update()</code> method is used to report the status of the light.

```csharp
using System;
using StateMachineDemo.States;

namespace StateMachineDemo
{
    public class Program
    {
        public static void Main(string[] args)
        {
            TrafficLight light = new TrafficLight();
            light.Activate();
            Console.WriteLine("Press ESC to stop");
            do
            {
                while (!Console.KeyAvailable)
                {
                    while (light.Running)
                    {
                        light.Update();
                    }
                }
            } while (Console.ReadKey(true).Key != ConsoleKey.Escape);
            light.Deactivate();
            Console.ReadLine();
        }
    }
}
```

## Context Interface
The simple interface <code>ITrafficLight</code> manages the "default" behavior that is exposed to the client.

```csharp
namespace StateMachineDemo{
    public interface ITrafficLight{
        void Activate();
        void Deactivate();
        void Update();
    }
}
```

## Context
In this example, the context class is our <code>TrafficLight</code> class, but we still use an interface <code>ITrafficLight</code> to manage default behavior. 
The <code>TrafficLight</code> class manages the objects current state with a private instance of our <code> ITrafficLightState </code> class called <code>State</code>. 
When the class is newed-up from the client, the constructor sets its state to the <code> RedLight </code> state.
In addition, this classes exposes the methods; <code>Activate()</code> <code>Update()</code> <code>Deactivate()</code> to the client. 
Within our <code>Update()</code>, the application calls the <code>Change()</code>, that intiates the transition from one state to the next.

```csharp
using StateMachineDemo.States;

namespace StateMachineDemo
{
    public class TrafficLight :ITrafficLight
    {   
         private ITrafficLightState _state;
        public bool Running { get; private set; }
 
        public TrafficLight()
        {
            _state = new RedLight();
        }
 
        public void Activate()
        {
            Running = true;
        }
 
        public void Deactivate()
        {
            Running = false;
        }
 
        public void Update()
        {
            _state = _state.Change();
        }
    }
}
```

## State
The simple interface <code>ITrafficLightState</code> manages the "default" behavior that is used within the concrete states.

```csharp
public interface ITrafficLightState
    {
        ITrafficLightState Change();
    }
```

## Concrete State Classes

Our Concrete State classes manage the specific implementation of each State (i.e. Green, Red, or Yellow light) For example, the <code>GreenLight</code> class
implements  <code> Change() </code> method by changing the state to a Red Light State by returning a new <code>RedLight</code> object, waiting for 30 seconds, and printing info to screen. 
Each concrete class manages thier implementation of the <code>ITrafficLightState</code> based on thats states needs. 

```csharp
using System;
using System.Threading;

namespace StateMachineDemo.States
{
    public class GreenLight : ITrafficLightState
    {
        public ITrafficLightState Change()
        {
            Console.WriteLine("Green Light - 30 second wait");
            Thread.Sleep(30000);
            return new YellowLight();
        }
    }
}
```

```csharp
using System;
using System.Threading;

namespace StateMachineDemo.States
{
    public class RedLight : ITrafficLightState
    {
        public ITrafficLightState Change()
        {
            Console.WriteLine("Red Light - 30 second wait");
            Thread.Sleep(30000);
            return new GreenLight();
        }

    }
}
```

```csharp
using System;
using System.Threading;

namespace StateMachineDemo.States
{
    public class YellowLight : ITrafficLightState
    {
        public ITrafficLightState Change()
        {
            Console.WriteLine("Yellow Light - 10 second wait");
            Thread.Sleep(10000);
            return new RedLight();
        }
    }
}
```
<a href="{{ site.url }}/behavioral/state" class="btn"> <i class="fa fa-arrow-left" aria-hidden="true"></i> Return to State Pattern</a>
