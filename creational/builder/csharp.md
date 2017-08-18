---
layout: article
title: Builder Pattern C# Example
modified:
categories: 
excerpt: 
tags: []
image:
  feature: 
  teaser:
  thumb:
---

<a href="{{ site.url }}/creational/builder" class="btn"> <i class="fa fa-arrow-left" aria-hidden="true"></i> Return to Builder Pattern</a>

![Builder Pattern](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Builder_UML_class_diagram.svg/640px-Builder_UML_class_diagram.svg.png)

To set-up this example, ASP.NET Core is used to create a Console Application. The full <a href="https://github.com/2joephillips/DPatterns-Examples/tree/master/creational/builder/csharp">C# code base</a> can be accessed from GitHub.

{% include toc.html %}

## Set-up
This simple console app is used to create a shop that can create different types of vehicles. The types consist of Scooter, Car, and Motorcycle. Once created the builder with call a Show() method that will display the parts of the vehicle.

```csharp
namespace csharp
{
    class Program
    {
        static void Main()
        {
            //The VehicleBuilder is 'Builder' 
            VehicleBuilder builder;
            //The shop is the 'Director'
            Shop shop = new Shop();

            //The ScooterBuilder, CarBuilder, and MotorcycleBuilder are the 'ConcreteBuilder' classes
            builder = new ScooterBuilder();
            shop.Construct(builder);

            //The Vehicle is the 'Product'
            builder.Vehicle.Show();

            builder = new CarBuilder();
            shop.Construct(builder);
            builder.Vehicle.Show();

            builder = new MotorcycleBuilder();
            shop.Construct(builder);
            builder.Vehicle.Show();
        }
    }
}
```
## Builder

The IVehicleBuilder is the interface used by the Director to build a product object.

```csharp
namespace csharp
{
    interface  IVehicleBuilder
    {
         Vehicle GetVehicle();
         void BuildFrame();
         void BuildEngine();
         void BuildWheels();
         void BuildDoors();
    }
}
```

## Director

The Shop class is used to construct an object based on the Builder Interface.

```csharp
namespace csharp
{
/// <summary>
/// The 'Director' class
/// </summary>
    internal class Shop
    {
        public void Construct(IVehicleBuilder vehicleBuilder)
        {
            vehicleBuilder.BuildFrame();
            vehicleBuilder.BuildEngine();
            vehicleBuilder.BuildWheels();
            vehicleBuilder.BuildDoors();
        }
    }
}
```

## Product
The Vehicle class is the representation of the complex object that is being built. The Concrete builder
classes build the product's internal representation and defines the process in which it is built. In addition, 
in this class it has a show method that can be called to display what the object looks like after construction.


```csharp
using System;
using System.Collections.Generic;

namespace csharp
{
    internal class Vehicle
    {
        private readonly string _vehicleType;
        private Dictionary<string, string> _parts = new Dictionary<string, string>();

        public Vehicle(string vehicleType)
        {
            this._vehicleType = vehicleType;
        }

        public string this[string key]
        {
            get { return _parts[key]; }
            set { _parts[key] = value; }
        }

        public void Show()
        {
            Console.WriteLine("\n---------------------------");
            Console.WriteLine("Vehicle Type: {0}", _vehicleType);
            Console.WriteLine(" Frame : {0}", _parts["frame"]);
            Console.WriteLine(" Engine : {0}", _parts["engine"]);
            Console.WriteLine(" #Wheels: {0}", _parts["wheels"]);
            Console.WriteLine(" #Doors : {0}", _parts["doors"]);
        }
    }
}
```


## Concrete Builder

The MotorcycleBuilder, CarBuilder, and ScooterBuilder, are the classes that hold the information 
to build that specific object. 

```csharp
using System;
using System.Collections.Generic;

namespace csharp
{
    internal class ScooterBuilder : IVehicleBuilder 
    {
        public ScooterBuilder() => vehicle = new Vehicle("Scooter");
        public Vehicle vehicle { get; set; }
        public void BuildDoors() => vehicle["doors"] = "0";
        public void BuildEngine() => vehicle["engine"] = "500 cc";
        public void BuildFrame() => vehicle["frame"] = "Scooter Frame";
        public void BuildWheels() => vehicle["wheels"] = "2";
        public Vehicle GetVehicle() => vehicle;
    }
}
```

```csharp
using System;
using System.Collections.Generic;

namespace csharp
{
    class MotorcycleBuilder : IVehicleBuilder
	{
		public Vehicle vehicle { get; set; }
        public MotorcycleBuilder() => vehicle = new Vehicle("MotorCycle");
        public void BuildFrame() => vehicle["frame"] = "MotorCycle Frame";
        public void BuildEngine() => vehicle["engine"] = "500 cc";
        public void BuildWheels() => vehicle["wheels"] = "2";
        public void BuildDoors() => vehicle["doors"] = "0";
        public Vehicle GetVehicle() => vehicle;
    }

}
```

```csharp
using System;
using System.Collections.Generic;

namespace csharp
{
    class CarBuilder : IVehicleBuilder
	{
		public Vehicle vehicle { get; set; }
        public CarBuilder() => vehicle = new Vehicle("Car");
        public void BuildFrame() => vehicle["frame"] = "Car Frame";
        public void BuildEngine() => vehicle["engine"] = "2500 cc";
        public  void BuildWheels() => vehicle["wheels"] = "4";
		public  void BuildDoors() => vehicle["doors"] = "4";
        public Vehicle GetVehicle() => vehicle;
    }

}
```