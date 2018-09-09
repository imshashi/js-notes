# Conceptual Aside

## Syntax Parsers
  ### A program that reads your code and determines what it does and if its grammer is valid.
  Your code isn't magic. Someone else wrote a program to translate it for the computer.
  These programs are called compilers/interpreters. Your code is not what's actually been given to computer but a translator of it(your code).

## Lexical Environments
  ### Where something sits physically in the code you write.
  'Lexical' means 'having to do with words or grammer'. A lexical environment exists in programming languages in which where you write something is important.

  For an example, in code written below, varible 'a' sits lexically inside the function 'hello'.

  ```js
  function hello() {
    var a = 'hello world';
  }
  ```

## Execution Contexts
  ### A wrapper to help manage the code that is running.
  There are lots of lexical environments. Which one is currently running is managed via execution contexts. It can contain things beyond what you've written in your code.


## Name/Value Pairs
  ### A name which maps to a unique value.
  The name may be defined more than once, but can have only one value in any given context.
  The value may be more name/value pairs.

  in code written below, 'address' is name and '58-B, Park Street' is it's value

  ```js
  address = '58-B, Park Street'
  ```

## Objects
  ### A collection of name value pairs
  The simplest definition when talking about Javascript.
  ```js
  address = {
    street: 'Main',
    number: 100,
    apartment: {
      floor: 2,
      number: 202
    }
  }
  ```

## The Global Environment And Global Object

  Whenever code is run in JS, its run inside an execution context.
  The base execution context is global execution context. It has couple of special things that come along. Global means the thing that's accessible everywhere to everything. Global execution context two things for you:
    global object('window' in browser)
    'this'

  These 2 things are created by js engine by default, without writing a single line of JS code. These 2 things are available to all code running inside opened browser window tab.

  For browsers case, these 2 things represent same thing, 'window' == 'this'

  * Global = 'Not inside a function' (in JS)

  if we write following code inside *.js file:

  ```js
  var a = 'Hello World!';

  function b() {
  }
  ```

  both variable 'a' and function 'b' are not inside any function so, these are global. In JS, when we write code which is not inside any function, then that code is attached to global object(window) or 'this'.
  So, in this case, we can access variable 'a' in following way:

  ```js
  a; // 'Hello World!'
  window.a; // 'Hello World!'
  ```

## The Execution Context: Creation & 'Hoisting'

  ```js
  var a = 'Hello World!';

  function b() {
    console.log('Called b!');
  }

  b(); // Called b!
  console.log(a); // Hello World!
  ```

  Output of above code is obvious and as per expectation. But notice following:

  ```js
  b(); // Called b!
  console.log(a); // undefined!

  var a = 'Hello World!';

  function b() {
    console.log('Called b!');
  }

  ```
  Execution context has two phases in JS engine.
    Creation: Set up the variables and functions in memory
    Code Execution: Runs your code line by line.

  ### Hoisting: Variables setup (and set equal to  'undefined') and Functions setup

## Single Threaded
  ### One command at a time
  Under the hood of the browser, may be not because js is not the only thing which is happening in the browser.

## Synchronous
  ### One at a time
  And in order...

  In JS, only one thing is happenning at a time.

## Function Invocation AND The Execution Stack
  ### Invocation: Running a function. In JS by using parenthesis (). like b();

## Variable Environment
  ### Where the variables live
  And how they relate to each other in memory. Every execution context has its own variable environment.

## Scope
  ### Where a variable is available in your code.

  Scope is the reference to outer environment that any running function has.


## The Scope Chain

  Consider the following code.:

  ```js
  function b() {
    console.log(myVar);
  }
  function a() {
    var myVar = 2;
    b();
  }

  var myVar = 1;
  a();
  ```

  The output of code written above is '1'.

  Where function sits lexically, determines its reference to outer environment. In given code, function 'b' is written/sits lexically in global scope, so it's reference to outer environment is global environment and thus has access to myVar in global environment with value 1.

  Now consider following code:

  ```js
  function a() {
    function b() {
      console.log(myVar);
    }
    var myVar = 2;
    b();
  }

  var myVar = 1;
  a();
  ```

  Now, in this updated code, function 'b' sits lexically in function a's execution context. So, it's reference to outer environment is function 'a' and hence has access to myVar with value 2 defined in function 'a'.
  function a's reference to outer environment is global environment.

  Now consider one more example:

  ```js
  function a() {
    function b() {
      console.log(myVar);
    }
    b();
  }

  var myVar = 1;
  a();
  ```

  Now, in this code, output would be 1. function 'b' doesn't have myVar defined in its scope, so it'll look into reference to its outer environment which is function a. Now, function 'a' also hasn't defined myVar in it's scope, so function 'b' will move to next reference to outer environment which is global environment. Global environment has defined myVar in it's scope, hence function 'b' used that value and output is '1'. This is how scope chain can be described.
