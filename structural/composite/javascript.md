---
layout: article
title: Composite Javascript Example
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

To set-up this example, I am injecting the Javascript into a index.html page, and having the <code>document.write()</code> display on any text on the page. 
The full <a href="https://github.com/2joephillips/DPatterns-Examples/tree/master/structural/composite/javascript" target="_blank">
Javascript Code Base</a> can be accessed from GitHub.

{% include toc.html %}

## Set-up
This simple web page  is used to compile workers with thier rating into teams that have supervisors. With the ability to print out the ratings of each worker within the team. In the scenario below we build a team 1 and then add it to another team to show how composite works. Then print all the workers ratings.


## Component

The Team function is the Component part of the Composite pattern. It declares varabiles for giving the team a name, array for employees, and the name of the supervisor. It also creates methods for adding new employees, setting up the team with a name and supervisor, and displaying the teams performance summary. 

```javascript
var Team = function () {
  var _employees = [];
  var _name;
  var _supervisor;
  return {
      setUp: function(name, supervisor){
          _name = name;
          _supervisor = supervisor;
      },
      add: function (employee) {
          _employees.push(employee)
      },
      performanceSummary: function () {
          document.write("<br>Team: " + _name + "<br>");
          document.write("Supervisor: " + _supervisor.name + "<br>");
          document.write("Members Reviews <br>");
          for (var i in _employees) {
              _employees[i].performanceSummary();
          }
      }
  };
}
```