---
layout: post
title:  "Autowire Interfaces"
date:   2016-12-23 23:28:47 +1100
tags: java spring autowired dependency injection
---
Spring lets you autowire all components implementing the interface.

```
@Component
public interface Animal {
   void talk();
}
```

```
public class Cat implements Animal {
  void talk() {
    System.out.println("Meow");
  }
}
```

```
class Dog implements Animal {
  void talk() {
    System.out.println("Bow wow");
  }
}
```

If you want to inject all implementations of `Animal` interface in some service, you can just inject a list of type Animal.

```@Autowired
private List animals;
```

The field `animals` is a list of all components implementing the `Animal` interface. Now if you want to invoke <code>talk()</code> method on Dog, Cat and other implementations of the <code>Animal</code> interface, you can do the following.

```
class SomeService {
  @Autowired
  private List animals;

  void someMethod() {
    animals.forEach(Animal::talk())
  }
}
```