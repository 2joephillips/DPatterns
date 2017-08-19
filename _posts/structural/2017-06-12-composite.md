---
layout: article
title: Composite
modified:
categories: structural
excerpt: "Create a tree structure to represent part as well as whole hierarchy."
tags: []
image:
  feature:
  teaser: patterns/composite.jpg
  thumb:
---

{% include toc.html %}

# Purpose

* Compose objects into tree structures to represent whole-part hierarchies. Composite lets clients treat infividual objects and compoisitions of objects uniformly.
* Recursive composition

Composite pattern is used to treat a group of objects in similar way as a single object. Composite pattern composes objects in terms of a tree structure to represent part as well as whole hierarchy.



# Structure
![State Pattern Structure](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/Composite_UML_class_diagram_%28fixed%29.svg/640px-Composite_UML_class_diagram_%28fixed%29.svg.png)

The UML class diagram above describes an implementation of the Composite design pattern.  

* **Component** declares the interface for objects in the composition by implementing default behavior common to all classes. In addition, it declares an interface for accessing and managing its child components.
* **Leaf** represents objects in the composition that have no children.
* **Composite** defines behavior for components having children and stores child components. Also, implements child-related operations in the Component interface.


![Example]({{ site.url }}/images/patterns/composite-feature.png)

# Example 

A good example of the Composite Pattern is a team/division hierarchy. Each worker is part of a team, and that team can be part of a larger team. 
Some workers can be Supervisors. 
The link below show an example of an implementation of an application that assigns workers to teams, and prints out the workers preformance rating.

[C# Example]({{ site.url }}/structural/composite/csharp/)

[Javscript Example]({{ site.url }}/structural/composite/javascript/)