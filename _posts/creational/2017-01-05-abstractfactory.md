---
layout: article
title: Abstract Factory
modified:
categories: creational
excerpt: "Create different types of concrete objects"
tags: []
image:
  feature:
  teaser: nav/400X250.png
  thumb:
published: true
---

{% include toc.html %}

# Purpose

* Separate object creation from the decision of which object to create
* Add new products and functionality without breaking Open Closed Principle

The purpose of the Abstract Factory is to provide an interface for creating families of related objects, without specifying concrete classes.

# Structure

![Abstract Factory](http://www.dofactory.com/images/diagrams/net/abstract.gif)

The UML class diagram above describes an implementation of the Abstract Factory design pattern.  

* **Abstract Factory** declares an interface for operations that create abstract products.
* **Concrete Factory** implements the operations to create concrete product objects.
* **Abstract Product** declares an interface for a type of product.
* **Product** defines a product object to be created by the corresponding concrete factory and implements the Abstract Product interface.


