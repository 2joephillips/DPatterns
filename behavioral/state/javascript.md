---
layout: article
title: State Javascript Example
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

To set-up this example, I am injecting the Javascript into a index.html page, and using <code>document.write()</code> to display information on the page. 
The full <a href="https://github.com/2joephillips/DPatterns-Examples/tree/master/behavioral/state/javascript" target="_blank">Javascript Code Base</a> 
can be accessed from GitHub.

{% include toc.html %}

## Set-up
Within the page, I am using a script tag to maintain all the JavaScript . To start the application, I am using <code>window.onload</code> to call a simple function that will use <code>document.write</code> to print two sentences on the screen. Then it will create a new TrafficLight object and then call the start method.

```javascript
window.onload = function() {
    document.write("<h1> Behavioral State Javascript Example</h1><br>")
    document.write("Starting Trafficlight <br>")
      var light = new TrafficLight();
    light.start();
};
```

## Context Interface
Since vanilla javascript does not have Interfaces, we will not have this portion which normally has the default behavior that is exposed to the client. 

## Context
The context class is our <code>TrafficLight</code> object, that contains a function for <code>start() change()</code>. Along with a variable for storing the <code>currentState</code> and <code>count</code>. 

The change method is used to take in a new state, and then set that new <code>state</code> as the <code>currentState</code>. Then it runs the <code>currentState</code> run method. To stop this for running forever, the <code>count</code> variable is used to ensure that this only runs 10 times.

```javascript
var TrafficLight = function () {
    var count = 0;
    var currentState = new Red(this);

    this.change = function (state) {
        // limits number of changes
        if (count++ >= 10) return;
        currentState = state;
        currentState.run();
    };

    this.start = function () {
        currentState.run();
    };
}
```

## State
Since vanilla javascript does not have Interfaces, we will not have this portion which normally has the default behavior that is exposed to the client. 


## Concrete State Classes
Our Concrete State classes manage the specific implementation of each State (i.e. Green, Red, or Yellow light) For example, the <code>GreenLight</code> class
implements  <code> run() </code> method by using <code>document.write</code> to write a simple message to the screen to indicate the color, and then waits for couple seconds then calls the <code>light.change</code> method to change the state to a <code>YellowLight</code> state. Which starts this process over, with <code>RedLight</code> turning to <code>YellowLight</code> and then back to <code>GreenLight</code>

```javascript
var RedLight = function (light) {
    this.light = light;
 
    this.run = function () {
        document.write("Red --> for 30 Seconds <br>");
        setTimeout(function(){light.change(new GreenLight(light));}, 1000);
    }
};
```

```javascript
var YellowLight = function (light) {
    this.light = light;
 
    this.run = function () {
        document.write("Yellow --> for 10 seconds <br>");
        setTimeout(function(){light.change(new RedLight(light));}, 1000);
    }
};
```

```javascript
var GreenLight = function (light) {
    this.light = light;
    this.run = function () {
        document.write("Green --> for 30 Seconds <br>");
        setTimeout(function(){light.change(new YellowLight(light));}, 1000);
    }
};
```

<a href="{{ site.url }}/behavioral/state" class="btn"> <i class="fa fa-arrow-left" aria-hidden="true"></i> Return to State Pattern</a>