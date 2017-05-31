---
layout: post
title:  Inheritence in Javascript and the Protoype Chain 
date:   2017-05-31 23:13:55 +0000
---


Today, we're going to discuss the protoype chain in Javascript and how to use it for inheritence between different types of objects. First, know that JavaScript is a prototype-based object-oriented language whereas other languages such as Java, C++ or Ruby use traditional class systems.  Also know that almost everything in JavaScript is an object and every object has a property, _prototype_, which is linked to another object. *That* object will have it own prototype and so on until you hit the core Object prototype.  When you try to access a property of an object that it does not contain, JS will look through the prototype chain for the property.

```

	function Vehicle(color, numberOfWheels) {
		this.color = color;
		this.numberOfWheels = numberOfWheels;
	}

	var vehicle = new Vehicle('blue', 4);

	vehicle.color // 'blue'
	vehicle.numberOfWheels // 4
```

We can add properties to Vehicle by setting them as a property of Vehicle instances in the constructor (as shown above) or by simply adding them to the Vehicle prototype.

```

	function Vehicle(color, numberOfWheels) {
		this.color = color;
		this.numberOfWheels = numberOfWheels;
	}

	// This will be added to the Vehicle prototype, and will be accessible to all instances of Vehicle.

	Vehicle.prototype.startEngine = function() {
		console.log('Engine started.')
	}

	var vehicle = new Vehicle('blue', 4);

	console.log(vehicle.color); // 'blue'
	console.log(vehicle.numberOfWheels); // 4
	vehicle.startEngine(); // 'Engine started.'
```

Let's say we wanted to be more specific, like what type of vehicle it is and then be able to define properties speficifc to that type of vehicle that arent found in other types, like the differences between a Car, Motorcycle or Plane.  At the same time we don't want to have to rewrite the functions and properties we already have set under the Vehicle prototype above.

```
  ...
	
	function Airplane(color, numberOfWheels, wingspan) {
		Vehicle.call(this, color, numberOfWheels);
		this.wingspan = wingspan;
	}

  // Sets up the prototype chain to inherit from the Vehicle.prototype
	 
	Airplane.prototype = Object.create(Vehicle.prototype);
	
  // Identifies the construtor function instances of Airplane will have 
	
	Airplane.prototype.constructor = Airplane; 

	var plane = new Airplane('white', 18, 196);
	
	console.log(plane.numberOfWheels); // 18
	console.log(plane.startEngine()); // 'Engine started.'
	
```

Looking in the console:

<center><img src="https://i.imgur.com/gHZWWoc.png" alt="what image shows" height="200" width="400"></center>

We can verify the prototype chain is set up.  `plane` is an instance of `Airplane` which inherits from the Vehicle prototype which in turn inherits from the JS core Object prototype.  We also know that since the `Airplane` prototype does not have its own property of `startEngine()` JS is able to go through the prototype chain to finds that property in `Vehicle`.
