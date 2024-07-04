---
title: "The Similarities Between High-Level Programming Languages."
datePublished: Tue Jul 25 2023 08:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clki0b9bn000709l7hpbaczul
slug: the-similarities-between-high-level-programming-languages
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698058360571/9c37a6b3-e37f-49f3-8cc8-0ca6ae9547c0.png
tags: programming-ciovqvfcb008mb253jrczo9ye, programming-languages, concepts, programming-concepts, core-concepts

---

## TL;DR.

High-level programming languages share common concepts such as variables, data types, literals, data structures, operators, control flow, expressions, functions, and statements. Despite high-level languages having their own syntax, these familiar ideas are popular and are regularly adopted across the industry.

(This concept does not apply to machine languages and assembly languages.)

## An Introduction.

If you're lucky, you'll be given a "cheat sheet" when you begin your studies for a software engineering certificate. 30 years ago when I was given this single page of awesomeness I *truly didn't* understand the importance of this document. Self-taught developers may know these concepts and fantom their value. I know that I appreciate what I've learned when I have to *actively* work for it. But these nuggets of knowledge were simply handouts, a bit of theory that *might* help with completing my assignments.

> The purpose of this post is to identify the functionalities that are common across multiple high-level programming languages.

The following is an AI-generated simulation of that cheat sheet from 30 years ago.

You're welcome.

## The Big Picture.

I usually start with a Big Picture view and discuss the impact a post will have on my future. This time, it's different; the impact started 30 years ago. While studying electrical and electronic engineering in the early 1990s, there was a class I took called computer programming... Or something. During that class, we studied the following compiled languages: Turbo Pascal, Turbo C, Visual C++, and Delphi. (There was also an embedded systems class that I loved, but that's beside the point.) One purpose of the programming class was to separate the concept of programming from the practice of using programming languages. Here's the point: I look at programming languages as specific implementations of the ideas listed below. Yes, each language will have its own "special sauce", but below are the "meat and potatoes" of most high-level programming languages.

### Variables.

Variables are used to store and manipulate data in programs. They act as containers that hold values. Variables are declared with a name and often a data type. Then the variable may be assigned a value. The value within a variable can also change as the program runs.

All programming languages have some way of declaring and using variables. The syntax may differ between languages but the concept remains the same.

```plaintext
name = "John" # String variable
age = 30      # Integer variable 
price = 19.99 # Floating point variable
```

### Literals.

Literals (usually known as Constants) represent fixed values like numbers, strings and booleans. Literals allow me to inject unchanging values into my code, values that remain "constant" as the program runs its course.

```plaintext
123     // Integer literal  
"Hello" // String literal  
true    // Boolean literal
```

### Operators.

Operators allow me to manipulate variables and expressions. Common operators include arithmetic (+ - \* /), assignment (=), logical (&& || !), and comparison (== &gt; &lt; ===).

```plaintext
x + y      // Arithmetic operation (when x and y are numeric)
x = 5      // Assignment operation (5 is assigned to the x variable)
a && b = z // Logical operation (z is true if a and b are true)
x > y      // Comparison operation (x is grater than y)
```

> NOTE: Under certain conditions in specific languages, the arithmetic operator (+) may behave as an append operator.

### Data Types.

Programs store and manipulate different types of data. Integers, text, and floating point values are common examples of data types. A programming language will define the data types that variables can hold, e.g. integer, float, string, boolean, etc.

All languages define some basic data types that variables can hold. (Yes, even JavaScript can define five different data types.)

```plaintext
  let name = "John"     // String 
  let age = 30;         // Integer  
  let price = 19.99;    // Float
  let isActive = true;  // Boolean
```

> NOTE: JavaScript does not define different types of numbers, like integer, short, long, etc. Instead, numbers are stored as double precision floating point numbers, as defined by the IEEE 754 standard.

### Data Structures.

Common data structures include arrays, objects, lists, stacks, queues, and trees. The purpose of these structures is to store data in an organised manner (using indices, for instance) even though the data *itself* may be unorganised.

```plaintext
  const numbers = [1, 2, 3];      // Array 
  const user = { name: "John" };  // Object
```

### Control Flow.

Control flow includes if/else statements, for-while loops, ternary operators, and switch cases. These mechanisms allow my code to make decisions and repeat tasks.

```plaintext
  if (x > 0) {
     // do something
  } else {
     // do something else  
  }
```

### Expressions.

Expressions are units of code that evaluate to a value. Expressions typically use operators to manipulate values.

```plaintext
  x + y   // Expression that evaluates to a sum
  a && b  // Logical AND expression
```

> ***NOTE: Under certain conditions in specific languages, the arithmetic operator (+) may behave as an append operator.***

### Functions.

Functions allow me to organize my code into reusable chunks. Functions take inputs, perform some logic, and return outputs.

Functions are essential for organizing my code into recyclable blocks.

```plaintext
  function add(x, y) {
    return x + y;
  }
```

### Statements.

Statements, sometimes called procedures, are units of executable code that perform some action but do not return a value.

```plaintext
  x = 5; // Assignment statement
  if (x > 0) { // if statement
     y = 10;
  }
```

## The Results.

Most high-level programming languages share these fundamental concepts. While the syntax and implementation may vary between languages, these core ideas are important for anyone learning to program or transitioning between languages.

## In Conclusion.

Beyond the commonalities of high-level programming languages, lies the *real* power that drives our creations: Algorithms. These compact clusters of input/process/output magic are used to power the functionality of my software applications. Above are the programming concepts that give me something on which to drape these algorithms, like a clothesline (the concepts) for hanging my damp laundry (the algorithms). I may be the first person *ever* to associate computer algorithms with wet garments and linen.

Until next time: Be safe, be kind, be awesome.