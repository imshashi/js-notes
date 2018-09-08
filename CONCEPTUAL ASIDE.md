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

