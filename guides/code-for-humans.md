---
explains: What we should think of when writing code so the most important computer we work with—the human brain—can parse it effectively
---

# How to code for humans

**Good code is written for humans and executable by machines**. This means that the human brain understanding your code is just as important – if not more so – as a machine understanding it. By understanding what the human brain is good at, and what it is not so good at, we can write code that functions better and is more easily maintainable.

With your code you are decribing functionality so precise it can be executed by machines. However those machines are not the ones tasked with fixing the bugs when they arise. The compiler doesn’t care if you call a variable `e` or `fatalErrorCode`. However, another human (or you in the future) might be tasked with fixing a breaking bug, at which point `e` might make it very difficult to figure out what is going on.

Code is read more often than it's written and most developer time is spent chasing bugs. There is much to be gained from writing code that is easy to understand, both if you are familiar with the code or new to the team.

Here are some basic priciples that can help you write better code.

## Human coding guidelines

### Single Responsibility Principle

* Functions should do 1 thing, and do it well
> a computer programming principle that states that every module or class should have responsibility over a single part of the functionality – [Wikipedia: Single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle)

* Functions should be around a maximum of 10-15 lines
* Functions should never exceed 25 lines

Tip: Describe every function in a _docstring_, if you use “and” in your description you know it does two things and needs to be split up.

### Short term memory holds about 7 slots

An average human being can hold about 7 things in memory at a time. However, this is an average, so while some people might peak at 11, you might only be able to remember 4 that time you were hungover but had to fix a bug in production.

* Functions should not contain more than 7 variables, ideally less

### Don’t make me think

When reading code we need all of our brainpower to understand what it is doing, so write clearly and understandable.

* Avoid abbreviations
* Name functions and methods descriptively
* Use autocomplete to complete long names

---

## Inspiration and further reading

* [Writing Code for Humans by Ilya Dorman](https://medium.com/@ilyothehorrid/writing-code-for-humans-5b80a89f439c)
* [Write Code for Humans not Machines by Mario Fusco](http://programmer.97things.oreilly.com/wiki/index.php/Write_Code_for_Humans_not_Machines)
