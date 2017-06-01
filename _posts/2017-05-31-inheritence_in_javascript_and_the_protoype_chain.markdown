---
layout: post
title:  Inheritance in Javascript and the Protoype Chain
date:   2017-05-31 19:13:56 -0400
---


<center><a href="https://medium.com/@j.onCoding/prototypal-inheritance-in-js-3b03df2dc4c0"><font size="+3">View UPDATED article on medium.com</font></a></center>

Today, I’m going to talk about the prototype chain in Javascript and how to use it for inheritance between different types of objects. First, know that JavaScript is a prototype-based object-oriented language whereas other languages such as Java, C++ or Ruby use traditional class systems. Also know that almost everything in JavaScript is an object and every object has a property, `__proto__`, which is linked to another object. That object will have it own prototype and so on until you hit the core Object prototype. When you try to access a property of an object that it does not contain, JS will look through the prototype chain for the property.

To see this in action we can can use a constructor function to create a certain “type” of object we will be using in our app.

```
function Vehicle() {}

var vehicle = new Vehicle()
```
<center><img src='https://cdn-images-1.medium.com/max/800/1*RVZyo2G4gYT8h97ZfBs6eg.png'></center>

We can see in the console that the Vehicle prototype is already inheriting from the core Object prototype.

The constructor allows us to create multiple instances of the Vehicle prototype. Let’s add some properties to our Vehicle prototype.

```
function Vehicle(color, numberOfWheels) {
 this.color = color;
 this.numberOfWheels = numberOfWheels;
}

var vehicle = new Vehicle(‘blue’, 4);

vehicle.color // ‘blue’
vehicle.numberOfWheels // 4
```

We can add properties to Vehicle by setting them as a method of Vehicle instances in the constructor (as shown above) or by adding them to the Vehicle prototype via a prototype method.

```
function Vehicle(color, numberOfWheels) {
 this.color = color;
 this.numberOfWheels = numberOfWheels;
}

Vehicle.prototype.startEngine = function() {
  console.log('Engine started.');
};

var vehicle = new Vehicle('blue', 4);

console.log(vehicle.color); // ‘blue’
console.log(vehicle.numberOfWheels); // 4
vehicle.startEngine(); // ‘Engine started.’
```

It should be noted that it is generally best practice to to add functions for the prototype via a prototype method. Binding a function to this in the constructor will re-declare the function for every instance of Vehicle, whereas using a prototype method will only add it to the Vehicle prototype, saving memory amongst other things.

<center><img src='https://cdn-images-1.medium.com/max/800/1*JWnnvcKnpEe9GOmpeFhTlQ.png'></center>

Here we can see that `startEngine()` is accessible to the instance vehicle not as a property but as a prototype function.

<hr>

Let’s say we wanted to be more specific, like what type of vehicle something is and then be able to define properties specific to that type of vehicle that aren't found in other types, like the differences between a car, a motorcycle or a plane. At the same time, we don’t want to have to rewrite the functions and properties we already have set under the Vehicle prototype above.

We can therefore create another constructor and set it to inherit from Vehicle. Using Airplane as an example:

```
...
function Airplane(color, numberOfWheels, wingspan) {
 Vehicle.call(this, color, numberOfWheels);
  this.wingspan = wingspan;
}
 
Airplane.prototype = Object.create(Vehicle.prototype); 
Airplane.prototype.constructor = Airplane;

var plane = new Airplane('white', 18, 196);
 
console.log(plane.numberOfWheels); // 18
console.log(plane.startEngine()); // ‘Engine started.’
```

There’s a lot happening here so let’s break it down.

First, we use `Vehicle.call` to allow instances of Airplane to be able to chain the settings in the Vehicle constructor (learn more about uses for `.call` [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)). This is all well and good but with this alone we still haven’t set up a proper prototype chain and proper inheritance.

<center><img src='https://cdn-images-1.medium.com/max/800/1*zdP5yHC_M23E03kPgk5Xmg.png'></center>

We can see here that Airplane is able to set `color` and `numberOfWheels`, accessed from `Vehicle.call`, as well as its own setter `this.wingspan`. However, its still not inheriting from the Vehicle prototype and does not have access to `startEngine()`.

```
Airplane.prototype = Object.create(Vehicle.prototype);
```

This is where the magic starts. [Object.create()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create/) actually sets up the prototype chain. By using Vehicle.prototype as a parameter we are setting the objects of the Airplane prototype to be an instance of the Vehicle prototype. Don’t believe me?

<center><img src='https://cdn-images-1.medium.com/max/800/1*dSIolURdR_meRkMwZ31l1Q.png'></center>

Looking further into our current instance of plane we can see the Airplane prototype now has Vehicle as a parent prototype and has access to startEngine().

```
Airplane.prototype.constructor = Airplane;
```

While not required, we set the constructor so that the program knows to create an instance of Airplane and not Vehicle. Not having it can cause some issues as explained in[ this StackOverflow article](https://stackoverflow.com/questions/8453887/why-is-it-necessary-to-set-the-prototype-constructor).

With everything in place, let’s look in the console:

<center><img src='https://cdn-images-1.medium.com/max/800/1*vg3kKy0f8MFXcSjDzZB_Ng.png'></center>

We can verify that Airplane instances have the correct constructor, the prototype chain is set up and `plane` is an instance of Airplane which inherits from the Vehicle prototype which in turn inherits from the JS core Object prototype. We also know that since the Airplane prototype does not have its own property of `startEngine()` JS is able to go through the prototype chain to finds that property in Vehicle.
