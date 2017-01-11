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
Within the Client section, we new up the TrafficLight and give it a default state of <code>RedLight()</code>. Also, we wrap the calls within a simple for loop to stop it from running for ever...


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
            light.State = new RedLight();

            for(int count = 0; count < 9; count++){
                
                light.ReportState();
                light.Wait();
                light.Change();
            }

            Console.ReadLine();
        }
    }
}
```
## TrafficLight Class

In this example, the context class is our <code>TrafficLight</code> class. This class manages the objects current state with an instance of our <code> ITrafficLightState </code> class called <code>State</code>. 
The class also exposes it's "default"  behavior. In this case, it exposes the methods; <code>Change()</code> <code>Wait()</code> <code>ReportState()</code>. 

```csharp
namespace StateMachineDemo
{
    public class TrafficLight : ITrafficLightState
    {   
        public ITrafficLightState State {get;set;}
        public void Change(){
            State.Change(this);
        }

        public void Wait(){
            State.Wait();
        }
        public void ReportState(){
            State.ReportState();
        }
    }
}
```

## ITrafficLightState Class
The simple interface <code>ITrafficLightState</code> manages the "default" behavior for our objects.

```csharp
namespace StateMachineDemo{
    public interface ITrafficLightState{
        void Change(TrafficLight light);
        void Wait();
        void ReportState();
    }
}
```

## Concrete State Classes

Our Concrete State classes manage the specific implementation of each State (i.e. Green, Red, or Yellow light) For example, the <code>GreenLight</code> class
implements  <code> Change() </code> method by changing the state to a Red Light State. Each concrete class can have thier on implementation of the <code>ITrafficLightState</code> methonds.

```csharp
using System;
using System.Threading;

namespace StateMachineDemo.States
{
    public class GreenLight : ITrafficLightState
    {
        void ITrafficLightState.Change(TrafficLight light)
        {
            light.State = new RedLight();
        }
        void ITrafficLightState.Wait(){
                Thread.Sleep(30000);
        }
        void ITrafficLightState.ReportState()
        {
            Console.WriteLine("Green Light - 30 second wait");
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
        void ITrafficLightState.Change(TrafficLight light)
        {
            light.State = new YellowLight();
        }
        void ITrafficLightState.Wait(){
            Thread.Sleep(30000);
        }
        void ITrafficLightState.ReportState()
        {
            Console.WriteLine("Red Light - 30 second wait");
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
        void ITrafficLightState.Change(TrafficLight light)
        {
            light.State = new GreenLight();
        }
        void ITrafficLightState.Wait(){
            Thread.Sleep(10000);
        }
        void ITrafficLightState.ReportState()
        {
            Console.WriteLine("Yellow Light - 10 second wait");
        }

    }
}
```
