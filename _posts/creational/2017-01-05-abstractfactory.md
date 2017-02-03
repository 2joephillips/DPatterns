---
layout: default
title: "Abstract Factory"
modified:
categories: creational
excerpt: Creates an instance of several families of classes
tags: []
image:
  feature:
  teaser: nav/400X250.png
  thumb:
published: true
---

{% include toc.html %}

# Purpose

* Provides an interface for creating familes of related or dependent objects without specifying their concrete classes.

The Abstract Factory defines a Factory Method that encapsulates the <code>new</code> operator and the concrete, platform-specific, 
product classes. Each "platform" is then modeled with a Factory derived class. 

# Structure

![Abstract Factory](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/Abstract_factory.svg/517px-Abstract_factory.svg.png)

The UML class diagram above describes an implementation of the Abstract Factory design pattern.  

* **Abstract Factory** declares an interface for operations that create abstract products.
* **Concrete Factory** implements the operations to create concrete product objects.
* **Abstract Product** declares an interface for a type of product.
* **Concrete Product** defines a product object to be created by the corresponding concrete factory and implements the Abstract Product interface.


