---
layout: post
title: "Javascript Closures Explained"
permalink: /javascript-closures-explained
author: ben
---

<p>I first started learning about Javascript closures back when I was interviewing for a bootcamp in San Francisco.  This is a topic that commonly trips up newer developers and it is a favorite interview question used by many tech companies.  As I googled around it felt like I kept reading contradictory explanations and took me quite a while to finally make sense of what should have been a very easy concept to understand.</p>

<h3><strong>Here is the simplest explanation of a closure that I can manage:</strong></h3>
<br>
If function `foo` returns function `x`, function `x` remembers its original parent scope (`foo`) even if it is getting invoked in a completely different part of the code base.

<strong>Example:</strong>

```
var foo = function(){
  var x = 'Hello World!';  
  return function() {  
    alert(x);    
  }  
};

var bar = foo();

bar(); //alerts 'Hello World'
```
<br>
Notice that `foo` has finished executing and is closed by the time `bar` is invoked.  The function `foo` finishes executing and returns an anonymous function.  Despite the fact that `foo` is finished, the anonymous function being returned still retains access to the variable `x`.  The variable `x` is not deleted by the garbage collector.  This means that you have greater flexibility with how you write your functions.  You don't have to worry about any of your functions losing access to variables over the course of your program.  Your functions will behave the way that they appear at the time of writing.
<br>

You can also use closures to create private variables when creating classes.  The scope where `bar` is called has no knowledge of and no way to access the variable `x`.

-----

We teach a <a href="/full-time">full-time</a> and <a href="/part-time">part-time</a> online course on full-stack JavaScript development.  Over 13 weeks we cover data structures, algorithms, ES6, React/Redux, responsive design, node, testing, security, relational and non-relational databases, and more.  We also teach an introduction to cross platform mobile development using React Native and an introduction to machine learning using neural networks and brain.js.  Apply <a href="/apply">here</a> to set up a time to meet with one of our instructors to learn more about the course.
