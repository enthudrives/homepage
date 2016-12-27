---
layout: post
title:  "Lambdas at the cost of readability"
date:   2016-12-23 23:48:47 +1100
tags: java spring autowired dependency injection
---
When a method has a for, if-else blocks, with Java 8, it is tempting to convert the whole block to a single statement with lambdas.

```
for (Book book : books) {
  if (book.isAvailable()) {
    System.out.println("Available book: " + book.getName());
  }
}
```

Most of the time, for and if blocks are a clear code smell. They make me wonder if there is room for refactoring there. With Java 8, the above for loop could be converted to this one-liner.

```
books
  .stream()
  .filter(Book::isAvailable())
  .map(Book::getName())
  .forEach(name -> System.out.println("Available book: " + name));
```

Woohoo. We have no for loops in code. Number of lines of code has been reduced. And, it doesn’t look like Java anymore :P

Sadly, this code doesn’t perform any better. And it is not very easy to understand this either. I like Lambdas. But they can easily become hard to understand.