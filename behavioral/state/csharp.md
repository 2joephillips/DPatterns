---
layout: article
title: State CSharp Example
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

```csharp
namespace StateMachineDemo
{
    public class TrafficLight
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

```csharp
namespace StateMachineDemo{
    public interface ITrafficLightState{
        void Change(TrafficLight light);
        void Wait();
        void ReportState();
    }
}
```

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

```

```csharp

```
<a href="https://github.com/2joephillips/DPatterns-Examples/tree/master/behavioral/state/csharp" target="_blank">C Sharp Code Base</a>