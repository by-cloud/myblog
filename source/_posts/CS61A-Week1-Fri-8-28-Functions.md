---
title: 'CS61A Week1 Fri 8/28: Functions'
date: 2020-10-23 05:39:17
categories:
- [cs61a]
tags: [cs61a, Note]
---
## Ch. 1.1

The high productivity of computer science is only possible because the discipline is built upon an elegant and powerful set of fundamental ideas.

All computing begins with representing information, specifying logic to process it, and designing abstractions that manage the complexity of that logic.

{% blockquote William Shakespeare, A Midsummer-Night's Dream %}

And, as imagination bodies forth

The forms of things to unknown, and the poet's pen

Turns them to shapes, and gives to airy nothing

A local habitation and a name.

{% endblockquote %}

### **Statement & Expression**

Uniform Resource Locator (URL), a location of something on the Internet.

Broadly, computer programs consist of instructions to either

1. Compute some value
2. Carry out some action

### **Function**

Functions encapsulate logic that manipulates data. A web address is a piece of data, and the text of Shakespeare's plays is another. The process by which the former leads to the latter may be complex, but we can apply that process using only a simple expression because that complexity is tucked away within a function.

### **Object**

An object seamlessly bundles together data and the logic that manipulates that data, in a way that manages the complexity of both.

In the end, we will find that all of these core concepts are closely related: functions are objects, objects are functions, and interpreters are instances of both.

### **Computer = Powerful + Stupid**

Be prepared for *errors*. While computers are tremendously fast and flexible, they are also extremely rigid. The nature of computers is described in [Stanford's introductory course](http://web.stanford.edu/class/cs101/code-1-introduction.html)

Programming is about a person using their real insight to build something useful, constructed out of these teeny, simple little operations that the computer can do.

### **Errors & Debugging**

Learning to interpret errors and diagnose the cause of unexpected errors is called *debugging*.

Some guiding principles of debugging are:

1. **Test incrementally**: Every well-written program is composed of small, modular components that can be tested individually. Try out everything you write as soon as possible to identify problems early and gain confidence in your components.
2. **Isolate errors**: An error in the output of a statement can typically be attributed to a particular modular component. When trying to diagnose a problem, trace the error to the smallest fragment of code you can before trying to correct it.
3. **Check your assumptions**: Interpreters do carry out your instructions to the letter — no more and no less. Their output is unexpected when the behavior of some code does not match what the programmer believes (or assumes) that behavior to be. Know your assumptions, then focus your debugging effort on verifying that your assumptions actually hold.
4. **Consult others**: You are not alone! If you don't understand an error message, ask a friend, instructor, or search engine. If you have isolated an error, but can't figure out how to correct it, ask someone else to take a look. A lot of valuable programming knowledge is shared in the process of group problem solving.

## Ch. 1.2

A programming language is more than just a means for instructing a computer to perform tasks. **The language also serves as a framework within which we organize our ideas about computational processes. Programs serve to communicate those ideas among the members of a programming community.** Thus, programs must be written for people to read, and only incidentally for machines to execute.

When we describe a language, we should pay particular attention to the means that **the language provides for combining simple ideas to form more complex ideas.** Every powerful language has three such mechanisms:

- **primitive expressions and statements**, which represent the simplest building blocks that the language provides,
- **means of combination**, by which compound elements are built from simpler ones, and
- **means of abstraction**, by which compound elements can be named and manipulated as units.

In programming, we deal with two kinds of elements: *functions* and *data*. (Soon we will discover that they are really not so distinct.) Informally, data is stuff that we want to manipulate, and functions describe the rules for manipulating the data. Thus, any powerful programming language should be able to describe primitive data and primitive functions, as well as have some methods for combining and abstracting both functions and data.

Infix notation: `1 + 2`

Call expression: `add(1, 2)`

The most important kind of compound expression is a *call expression*, which applies a function to some arguments. No ambiguity can arise, because the function name always precedes its arguments.

Function notation has three principal advantages over the mathematical convention of infix notation.

1. Functions may take an arbitrary number of arguments.
2. Function notation extends in a straightforward way to *nested* expressions, where the elements are themselves compound expressions. In nested call expressions, unlike compound infix expressions, the structure of the nesting is entirely explicit in the parentheses.
3. Mathematical notation has a great variety of forms, some of this notation is very hard to type! However, all of this complexity can be unified via the notation of call expressions.

### **Statements & Expressions**

- Statements
- Expressions
  - Primitive expressions (number, name, string) [2020, add, ‘hello’]
  - Compound expressions
    - Infix notation [1 + 2]
    - Call expressions (operator, operand list) [operator(operand, operand, … , operand), nested]
      - Library expressions [import]

A critical aspect of a programming language is the means it provides for using names to refer to computational objects. If a value has been given a name, we say that the name *binds* to the value.

In Python, we can establish new bindings using the assignment statement, which contains a name to the left of = and a value to the right

Assignment is our simplest means of *abstraction*, for it allows us to use simple names to refer to the results of compound operations. In this way, complex programs are constructed by building, step by step, computational objects of increasing complexity.

The possibility of binding names to values and later retrieving those values by name means that the interpreter must maintain some sort of memory that keeps track of the names, values, and bindings. This memory is called an *environment*.

Names can also be bound to functions. We can use assignment statements to give new names to existing functions. And successive assignment statements can rebind a name to a new value.

In Python, names are often called *variable names* or *variables* because they can be bound to different values in the course of executing a program. When a name is bound to a new value through assignment, it is no longer bound to any previous value. One can even bind built-in names to new values.

When executing an assignment statement, Python evaluates the expression to the right of = before changing the binding to the name on the left. Therefore, one can refer to a name in right-side expression, even if it is the name to be bound by the assignment statement.

```python
>>> x = 2

>>> x = x + 1

>>> x

3
```

We can also assign multiple values to multiple names in a single statement, where names on the left of = and expressions on the right of = are separated by commas.

```python
>>> area, circumference = pi * radius * radius, 2 * pi * radius

>>> area

314.1592653589793

>>> circumference

62.83185307179586
```

Changing the value of one name does not affect other names. Below, even though the name area was bound to a value defined originally in terms of radius, the value of area has not changed. Updating the value of area requires another assignment statement.

```python
>>> radius = 11

>>> area

314.1592653589793

>>> area = pi * radius * radius

380.132711084365
```

With multiple assignment, *all* expressions to the right of = are evaluated before *any* names to the left are bound to those values. As a result of this rule, swapping the values bound to two names can be performed in a single statement.

```python
>>> x, y = 3, 4.5

>>> y, x = x, y

>>> x

4.5

>>> y

3
```

### **Expression tree**

In computer science, trees conventionally grow from the top down. The objects at each point in a tree are called nodes.

Evaluating its root, the full expression at the top, requires first evaluating the branches that are its subexpressions. The leaf expressions (that is, nodes with no branches stemming from them) represent either functions or numbers. The interior nodes have two parts: the call expression to which our evaluation rule is applied, and the result of that expression. Viewing evaluation in terms of this tree, we can imagine that the values of the operands percolate upward, starting from the terminal nodes and then combining at higher and higher levels.

Next, observe that the repeated application of the first step brings us to the point where we need to evaluate, not call expressions, but primitive expressions such as numerals (e.g., 2) and names (e.g., add). We take care of the primitive cases by stipulating that

- A numeral evaluates to the number it names,
- A name evaluates to the value associated with that name in the current environment.

Notice the important role of an environment in determining the meaning of the symbols in expressions.

In general, statements are not evaluated but *executed*; they do not produce a value but instead make some change. Each type of expression or statement has its own evaluation or execution procedure.

A pedantic note: when we say that "a numeral evaluates to a number," we actually mean that the Python interpreter evaluates a numeral to a number. **It is the interpreter which endows meaning to the programming language.** Given that the interpreter is a fixed program that always behaves consistently, we can say that numerals (and expressions) themselves evaluate to values in the context of Python programs.

### **Pure functions**

Functions have some input (their arguments) and return some output (the result of applying them).

Pure functions are restricted in that they cannot have side effects or change behavior over time. Imposing these restrictions yields substantial benefits.

- First, pure functions can be composed more reliably into compound call expressions. We have seen that functions such as max, pow and sqrt can be used effectively in nested expressions.
- Pure functions tend to be simpler to test. A list of arguments will always lead to the same return value, which can be compared to the expected return value.
- Pure functions are essential for writing *concurrent* programs, in which multiple call expressions may be evaluated simultaneously.

### **Non-pure functions**

In addition to returning a value, applying a non-pure function can generate *side effects*, which make some change to the state of the interpreter or computer. A common side effect is to generate additional output beyond the return value, using the print function.

If you find this output to be unexpected, draw an expression tree to clarify why evaluating this expression produces this peculiar output.

### **Environment Diagrams**

Environment diagrams visualize the interpreter’s process.

How to draw a environment diagram:

<https://inst.eecs.berkeley.edu/~cs61a/sp13/pdfs/environment-diagrams.pdf>

<http://albertwu.org/cs61a/notes/environments.html#built-in-functions>

<http://markmiyashita.com/cs61a/environment_diagrams/>

<https://berkeley-cs61as.github.io/textbook/how-to-draw-environment-diagrams.html>

<https://inst.eecs.berkeley.edu/~cs61a/su10/resources/Joshua%20Cantrell%20Notes/8-EnvDiagrams.pdf>

### **Defining Functions**

Assignment is a simple means of abstraction: binds names to values.

Function definition is a more powerful means of abstraction: binds names to expressions.

```text
def <name>(<formal parameters>):
    return <return expression>
```

Function *signature* indicates how many arguments a function takes.

Function *body* defines the computation performed when the function is applied.

Execution procedure for def statements:

1. Create a function with signature \<name>(\<formal parameters>)
2. Set the body of that function to be everything indented after the first line
3. Bind \<name> to that function in the current frame

### Calling User-Defined Functions

Procedure for calling/applying user-defined functions (version 1):

1. Add a local frame, forming a new environment
2. Bind the function's formal parameters to its arguments in that frame
3. Execute the body of the function in that new environment

> A function’s signature has all the information needed to create a local frame.

### Looking Up Names in Environments

Every expression is evaluated in the context of an environment.

So far, the current environment is either:

- The global frame alone, or

- A local frame, followed by a global frame.
  
> ***Most important two things I'll say all day:***
>
> 1. An environment is a series of frames.
>
> 2. A name evaluates to the value bound to that name in the earliest frame of the current
environment in which that name is found.

E.g., to look up some name in the body of the square function:

- Look for that name in the local frame.
- If not found, look for it in the global frame.
(Built-in names like “max” are in the global frame too,
but we don’t draw them in environment diagrams.)
