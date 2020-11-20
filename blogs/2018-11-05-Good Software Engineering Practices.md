---
layout: post
title: Good Software Engineering Practices
date: 2018-11-05
---

# Good Software Engineering Practices

This is a summary of good software engineering practices, especially for data scientists.

## Start with requirement analysis and architecture design

Architecture first. Writing code without thinking of its architecture is useless in the same way as dreaming about your desires without a plan of achieving them.
Before writing the first line of the code, you should understand what it will be doing, how, what it will use, how modules, services will work with each other, what structure will it have, how it will be tested and debugged, and how it will be updated.


## Use good coding style, even not for production code

Below is a summary of good coding style:
- Always use descriptive names for variables and functions so that readers can tell the function of the code with as little documentation as possible.
- Modularity. Break the program down into self‐contained parts that have clear functions, which can be shared across different sections of the code.
- Avoid having excessive indentation, such as loops within loops within loops.
- Use comments when appropriate. If you do something bizarre in your code, explain why in a comment. Also, every file should ideally start with a comment that explains what it does. However, don’t overuse comments. They distract from the code itself, which should be mostly clear enough that you can read it directly. Comments can also be wrong or out of date, so leave them out if the code speaks for itself.
- If you have several blocks of code that do very similar things, it often pays to refactor them into a single routine.
- Try to separate boilerplate information (such as the way data is formatted) from the core processing logic of the program. For example, the order of columns in a table should usually be specified separately from the code, which processes the table.

## Important Coding Principles
- Keep it simple, stupid (KISS)

     When optimization challenges simplicity, simplicity wins.

- You aren’t gonna need it (YAGNI)

    If you have an ample chance of not coding what you don’t need right now, don’t do it. Try to make things step by step.

- Don’t repeat yourself (DRY) 

    Its underlying idea is that you have to avoid and reduce repetitions and redundancy by replacing those with abstractions or utilizing data normalization. For example, pseudocode is an excellent way to make sure you aren’t making any repetitions. You might be duplicating a bit of logic here or there, but you may want to merge them into a single function. For that reason, there’s only one mantra here — avoid repeating yourself in your code. 

- Write defensively

    Always think about what can go wrong, what will happen on invalid input, and what might fail, which will help you catch many bugs before they happen.

- Refactor

    Refactor whenever you see the need and have the chance. Programming is about abstractions, and the closer your abstractions map to the problem domain, the easier your code is to understand and maintain. 

- Version control for better tracking.
- Automation as much as possible.

    Automation is a 100% success in a long term. So if you have resources to automate something right now it should be done.

- Documentation.

    Do it well so that other people can understand what you are doing easily.

## Code Review

The purpose of code review is to improve the code quality, not to learn the code. It is more useful to ask people who is part of the project to do the code review rather than someone else who is new to the code.

## Test

Test is an essential part of the code to gurantee the success of the code development. 


References:
1. https://www.cs.utexas.edu/~mitra/csSummer2014/cs312/lectures/bestPractices.html
2. https://opensource.com/article/17/5/30-best-practices-software-development-and-testing
3. https://litslink.com/blog/what-are-software-engineering-best-practices
4. https://blog.k2datascience.com/software-engineering-fundamentals-best-practices-b5105d155c6d
