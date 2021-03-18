---
title: S.O.L.I.D For Human Beings
description: A digestible explanation of the S.O.L.I.D principles.
layout: post
categories: [programming]
---
S.O.L.I.D is an acronym in Object Orientation that comes up both in technical tests and in the wild in open source or proprietary code, however trying to get to grips with it can be daunting since we are often faced with definitions like this:

>If S is a subtype of T, then objects of type T may be replaced with objects of type S (i.e. an object of the type T may be substituted with its subtype object of the type S) without altering any of the desirable properties of that program.

This makes it extremely challenging for new programmers, who can really benefit from S.O.L.I.D to learn from and promote better code, so I’ve put together a little collection of simple examples which might be a little bit more digestible.

NOTE: These definitions are in no way academic or comprehensive, it’s just the way I think of them in my own way. Don't @ me.

- [Single Responsibility Principle](#srp)
- [Dependency Inversion](#di)
- [Liskov Substitution](#liskov)
- [Interface Segregation](#seg)
- [Open / Closed Principle ](#openclosed)

## Some definitions
We often talk about 'loose coupling' and 'high cohesion' a lot in programming, but it can seem quite weird and difficult to get your head around. I'll reference it a bit through this article so let's first have a look at what those terms actually mean.

In physics cohesion can be defined as
> 'the sticking together of particles of the same substance.'

This is good enough for us, because in programming we can take it to mean 'the sticking together of code of the similar intention'. If you have a Cat class, and it has a miaow, a walk and purr method it's probably highly cohesive. If you have a Cat class with 30 methods including fly, talk and other unrelated behaviour to a cat it's probably not very cohesive. Code that is similar wants to stick together.

We can define coupling as
>'a measure of how closely connected two bits of code are.'

If you change the walk method on your Cat class, and the purr method also has to change, it's probably very highly coupled code.

## S - Single Responsibility Principle <a name="srp"></a>
We should aim to make our classes only responsible for one coherent set of properties with related behaviours. We don’t want our class to be affected by changes that should not concern it because it’s full of properties and methods that really don’t belong there, and may change more than the class itself needs to.

The more we have to change, the more likely we are to introduce new bugs and probably the more unit tests we have to update. If we adhere to the loose coupling, high cohesion principles, we should have code that adheres to the Single Responsibility Principle.

### Before
Have a read of the code [here](https://github.com/outragedpinkracoon/SOLID-for-humans/tree/master/Single%20Responsibility%20Principle/before) before you continue.

We have an Athlete that has a totalDistance property that rightfully belongs there, and it has a run() method which belongs there which increments with this property.

However, it also has a writeDistanceLog() which is a bit naughty. Should the Athlete be responsible for this? Should the athlete care how the log is written? This is current breaking quite a few rules:

- It’s tightly coupled to the System.out console logging. What if we want to write to a file? We’d have to change the class.
- The Athlete is tied to this implementation. If we change the message we log, the Athlete has to change.

We’ve identified at least 2 reasons for the Athlete to change, none of which even relates to the state of the Athlete - the run() method or totalDistance property. We could imagine the Athlete having to change if we added a new behaviour, like sprint() or drinkWater(), but having to alter it’s source code because we want to write to a file instead of the console breaks the Single Responsibility Principle.

### After
Now check the refactored code [here](https://github.com/outragedpinkracoon/SOLID-for-humans/tree/master/Single%20Responsibility%20Principle/after).

In the refactored version, the athlete only has 1 method run() which we would expect. The code to handle logging the distance has been abstracted away to an AthleteConsoleLog. We don’t care how the log achieves it goal, all we care about is that the athlete has some way to make a log entry.

Now, if we want to change the way the athlete logs to use a file instead of the console _we don’t need to change the Athlete class itself_. If we want to change the message in the log, _we don’t need to change the Athlete class itself_.

This is great news since all the athlete has to care about now is it’s own properties and methods that act on them and not the specifics of how the log works.

## Dependency Inversion <a name="di"></a>
A dependency is another class that our class needs to use in order to function.

Dependency Inversion is where we never “new” anything up in a class, and we pass it in from the class that instantiates it. This stops code having an opinion about the implementation details of a dependency.

### Before
Read the code [here](https://github.com/outragedpinkracoon/SOLID-for-humans/tree/master/Dependency%20Inversion/before) before continuing.

The Athlete is newing up an AthleteConsole log itself. It is taking ownership over this and deciding what kind of implementation it should use. It’s having an opinion about how the internals of another class works that it relies on. In this case, we want a log that writes to the terminal.

The problem with this, is that if we decide we want a different kind of log that writes to a file? We’d have to change the actual Athlete and new up a different kind of log. What if we have 2 athletes that log in different ways? Nightmare.

An Athlete doesn’t really want to have to care about what kind of log it’s using, it just wants to use it.

### After
Now read the code [here](https://github.com/outragedpinkracoon/SOLID-for-humans/tree/master/Dependency%20Inversion/after).

The Athlete has been changed to rely on _an interface_ AthleteLog instead of a _concrete class_ AthleteConsoleLog. This allows us to pass any class which implements this interface into the Athlete when we create it. This means we can easily change the kind of log an Athlete writes, by passing it a valid class.

In the runner, we pass a new Athlete an AthleteConsoleLog. We then create a new Athlete that uses an AthleteFileLog. We have _changed the behaviour_ of an Athlete without modifying _the source code_ of the Athlete itself.

## Liskov Substitution <a name="liskov"></a>
Whenever we choose to extend an abstract class or implement an interface, we are saying that we will adhere to the contract. We must implement all the methods to allow the class using the contract act to as if it is the super class type it has been given. This is easier explained with an example.

### Naughty
Read the code [here](https://github.com/outragedpinkracoon/SOLID-for-humans/tree/master/Liskov%20Substitution/bad).

Our AthleteLog has a distance() method, so we expect both the AthleteConsoleLog and AthleteFileLog that implement it to have a distance method that does something sensible.

All we know in our Athlete is that the AthleteLog interface has a distance() method that we are going to use. Anything that can be declared as an AthleteLog type must provide this implementation for us to use, so we can swap in and out different classes if we need to.

E.g both of these are valid:

```java
AthleteLog log = new AthleteConsoleLog();
AthleteLog log = new AthleteFileLog();
```
Both the AthleteConsoleLog and AthleteFileLog can be declared as an AthleteLog. Thus, we expect both of them to have a distance() method, just like AthleteLog says it should.

However we are in for a nasty surprise…

When we use the AthleteConsoleLog, we get a horrible RuntimeException. Why? It turns out the naughty programmer who implemented the interface and made us trust that the implementation was in the AthleteConsoleClass, adhering to the contract, threw an exception instead of doing something sensbile and making the logging happen.

This breaks the Liskov Substitution principle. Any class implementing AthleteLog must have a valid implementation of distance(). If it doesn’t, then it should not be using the interface in the first place. We can’t trust AthleteConsoleLog to be used in conjunction with AthleteLog as a type, as we declared in the example above.

We don’t want to give other developers a nasty surprise when they try to use our class, which is pretending to be adhering to acontract when it’s really not.

This also applies to overloading superclass methods and making them throw errors or return unexpected things.

### Good
Now go check the code [here](https://github.com/outragedpinkracoon/SOLID-for-humans/tree/master/Liskov%20Substitution/good).

In the good example, both the AthleteConsoleLog and the AthleteFileLog have valid distance() methods, and can both be interchanged with AthleteLog as a type. All is good. NO missing methods, no weird returns. We can trust it to do what we expect from an AthleteLog, which is to run the distance() method it promises to us.

## Interface Segregation <a name="seg"></a>
We should always favour smaller _highly cohesive_ interfaces over larger less specific ones. A larger set of methods on an interface can result in breaking the Liskov Substitution principles, since the class using it may not need all of the methods defined on it and choose to do nothing, throw an exception etc

We shouldn’t force methods onto classes that they do not need.

### Before
Read the code [here](https://github.com/outragedpinkracoon/SOLID-for-humans/tree/master/Interface%20Segregation/before).

The Sprinter is implementing the Olympian interface. It uses the drinkWater(), sprint() and jumpHurdle() methods as we’d expect. However, the interface also has a bunch of other completely unrelated methods like swim() and pedal() which are useless to the Sprinter, but the Sprinter must implement them to use the Olympian type.

This results in lots of unused methods and throwing exceptions, which is untidy and breaks the Liskov Substitution Principle.

This interface has _too low cohesion_.

### After
Have a look at the refactored code [here](https://github.com/outragedpinkracoon/SOLID-for-humans/tree/master/Interface%20Segregation/after).

The Olympian interface has been spread out into 3 separate, _highly cohesive_, interfaces of related behaviour.

The sprinter only has to implement the methods of an Olympic Runner, which make sense for it.

## Open / Closed Principle <a name="openclosed"></a>
We want to be able to cope with changes in the behaviour of our code, but making the smallest possible changes to the source code as possible to achieve this. We don’t a tiny alteration in how our program runs to cause us to have to update hundreds of lines of code.

The Open Closed Principle encourages us to keep our code “open for extension but closed for modification”. We seen this with dependency inversion - we can pass in different behaviours to a class without altering it directly.

The [template pattern](http://www.tutorialspoint.com/design_pattern/template_pattern.htm) is another great example of this - we can change the behaviour of a super class by delegating methods to the subclass. The superclass doesn’t have to change, but can be used effectively to abstract away details from the subclass.

### Before
Have a look at the code [here](https://github.com/outragedpinkracoon/SOLID-for-humans/tree/master/Open%20Closed%20Principle/before).

A Gymnast and a Boxer are both athletes that compete in events. Entering an event has a specific turn of events:

Warm up
Compete
Calculate Points
Recieve Medal
These have to happen in this order. This is a fairly crude example with the same point system being used for assigning medals to both Gymnasts and Boxers.

We can see there is a lot of duplication - both the Gymnast and Boxer have a points property and both have the same prepare(), compete() and recieveMedal() methods. This is not DRY. If we want to add another type of Athlete, we need create a whole new class and duplicate all of these methods, just for the sake of adding a slightly different points calculation.

If we change the prepare() method on the Boxer, we also need to change it in the Gymnast since they are both meant to be the same. The classes are open for modification since any changes to the other class means it has to be updated. Entering an event cannot be easily extended, since any new action must be added to both a Gymnast and a Boxer.

### After
Read the refactored code [here](https://github.com/outragedpinkracoon/SOLID-for-humans/tree/master/Open%20Closed%20Principle/after).

All of the common methods have been pushed up into the new Athlete abstract class. There is an abstract method calculatePoints() that delegates it’s implementation to the Gymnast and the Boxer. This sets the points property which is used in the recieveMedal() method of the Athlete class.

This is super cool, since adding a new type of Athlete is dead easy. We just extend the Athlete class and write the required calculatePoints() method. The Athlete class is closed for modification since it has all of the running order information inside of it and we do not need to alter the source code to add a new type of athlete. If we didn’t have the source code for an Athlete, we could still make a Swimmer that extends it.

The Athlete is open for extension since we can implement the calculatePoints() method on the class extending it, to define what the behaviour should be without touching the source code of the parent class which is responsible for running the enterEvent() method.

## Conclusion

The S.O.L.I.D principles have been around a long time and are often fodder in technical interviews but can also often be found used in the wild in open source projects and frameworks. Hopefully your new understanding will help you recognise them when you see them, and give you the confidence to dabble in them when it makes sense in your own code.
