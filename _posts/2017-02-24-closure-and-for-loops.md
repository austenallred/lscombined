---
layout: post
title: "Closure and For Loops"
permalink: /closure-and-for-loops
author: ben
---

Note: If you don't understand Javascript closures then I recommend you first check out [this](https://lambdaschool.com/javascript-closures-explained) blog post.

While interviewing for a job in San Francisco I was asked to fix the following code:

```````
for (var i = 1; i <= 5; i++) {
  setTimeout(function(){
    console.log(i);
  }, 100);
}
````````
<br>
The intended result is for five timeouts to print 1, 2, 3, 4, 5 in order after 100 milliseconds. If you run the above code the number 6 will print to the console five times.  Can you tell what's wrong?

-----

The problem here is that the closure scope for each anonymous function at each iteration of the loop points to the same variable, the same spot in memory. They're all pointing to a single `i`.  When 100 milliseconds pass and the callback functions begin to run they all go and look for the variable `i` on their parent scope.  All of the callback functions share the same parent scope that has a single `i` variable which is now 6.  `i` is 6 because that is the number that finally breaks the loop.
<br>

By using an IIFE, Immediately Invoked Function Expression, you can create a "block scope" of sorts that is unique to each anonymous function.  Each anonymous function then points to its own unique `i` variable.
<br>

<strong>Solution:</strong>

`````
for (var i = 1; i <= 5; i++) {
  (function(i){
    setTimeout(function(){
      console.log(i)
    }, 100);
  })(i);
}
`````
<br>
Passing `i` to the IIFE creates a copy of `i` in the IIFE's scope.  The IIFE is now the direct parent to the callback function.  There are five timeouts being created that each have their own unique IIFE as its direct parent.  Each IIFE has a separate copy of `i` that reflects the iteration of the loop where the timeout was created.

-----

We teach a <a href="/full-time">full-time</a> and <a href="/part-time">part-time</a> online course on full-stack JavaScript development.  Over 13 weeks we cover data structures, algorithms, ES6, React/Redux, responsive design, node, testing, security, relational and non-relational databases, and more.  We also teach an introduction to cross platform mobile development using React Native and an introduction to machine learning using neural networks and brain.js.  Apply <a href="/apply">here</a> to set up a time to meet with one of our instructors to learn more about the course.
