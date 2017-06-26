---
layout: post
title: "Javascript Hoisting Explained"
permalink: /javascript-hoisting-explained
author: ben
---


A common question that people have when learning Javascript is what the difference is between a function expression and a function declaration.  (A function expression is where you take an anonymous function and assign it to a variable.  A function declaration is just a named function that you write out.)

For example:

Function Expression
`````
var x = function(){
  return true;
};
`````
Function Declaration
`````
function x(){
  return true;
}
`````
Obviously they are written differently but is there any difference in their behavior?
The key difference between these two patterns has to do with variable hoisting.  Variable hoisting is something that happens when your Javascript is compiled on the fly by the browser.  The browser reads your code and grabs all of your function and variable declarations and moves them to the top of the scope.

Like this:

`````
(function(){

  var a = true;
  var b = true;

  var c = function(){
    return true;
  };

  function d(){
    return true;
  }

})();
`````
Gets compiled to this for when the code is executed:
`````
(function(){

  function d(){
    return true;
  }
  var a;
  var b;
  var c;

  a = true;
  b = true;

  c = function(){
    return true;
  };

})();
`````

Notice how the function declaration was moved to the top of the scope.  Variable and function declarations are hoisted to the top.  Assignments stay where they are.  The anonymous function being assigned to the variable `c` still happens in its original location.


A Common Gotcha:
-------------------------------

The following code throws an error:

`````javascript
(function(){

  a();
  b();//Uncaught TypeError: undefined is not a function

  function a() {
    return true;
  }

  var b = function(){
    return true;
  };

})();
`````
The reason we get an error is because `var b` is hoisted but not the anonymous function that is on the right side of the expression.

Here's what that code looks like at runtime with its declarations hoisted:
`````
(function(){

  function a(){
    return true;
  }
  var b;

  a();
  b();//Uncaught TypeError: undefined is not a function

  b = function(){
    return true;
  };

})();
`````

As you can see the variable `b` has not had anything assigned to it at that point in the script's execution so it is `undefined` and throws an error when you try to invoke it.

My advice is to pick one style and stay consistent.  When first learning JavaScript I encourage my students to start with only function expressions because it avoids any confusion caused by being able to invoke a function declaration before the line where it is written.

-----

We teach a <a href="/full-time">full-time</a> and <a href="/part-time">part-time</a> online course on full-stack JavaScript development.  Over 13 weeks we cover data structures, algorithms, ES6, React/Redux, responsive design, node, testing, security, relational and non-relational databases, and more.  We also teach an introduction to cross platform mobile development using React Native and an introduction to machine learning using neural networks and brain.js.  Apply <a href="/apply">here</a> to set up a time to meet with one of our instructors to learn more about the course.
