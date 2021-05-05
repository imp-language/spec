# Imp Language Specification

Imp is a general-purpose programming language originally implemented as a compiler for the Java Virtual Machine.

This is the official specification for the Imp programming language. It specifies

- the representation of Imp programs
- the syntax of the Imp language
- the semantics for executing Imp programs

This standard does not specify

- the method by which Imp programs are compiled
- the target platform to which Imp programs are compiled to
- the algorithms used for compilation


# Notation

The syntax is specified using ANTLR `.g4` syntax.

# Lexical Elements

## Comments

There are three forms of comments in an Imp program:

- *Line comments* start with `//` and stop and the end of the line
- *Multiline comments* start with `/*` and end with the first `*/` encountered.
- *Doc comments* start with `/**` and end with the first `*/` encountered. For more information on documentation comments, see the [TODO](TODO) section.

## Identifiers

Identifiers name entities such as variables, functions, and classes.

## Keywords

These words are reserved for language constructs and may not be used as identifiers.

- `loop`
- `if`
- `else`
- `function`
- `return`
- `val`
- `mut`
- `bool`
- `int`
- `char`
- `string`
- `export`
- `import`
- `from`
- `as`
- `new`
- `class`
- `interface`
- `enum`
- `public`
- `in`

## Operators

These sequences represent operators and punctuation

- TODO


## Literals

In an Imp program, primitive data types can be represented in a concise manner.

### Boolean Literals

Simply using the reserved keywords `true` or `false` defines a boolean value.

### Integer Literals

Base 10 integer literals are represented by the following ANTLR grammar:

```g4
 ([1-9] [0-9]*) | '0';
```

Essentially, any number that does not start with 0, or 0. Below are examples of valid integers.

```c
int_lit_number = 123457
int_lit_1 = 1
int_lit_0 = 0
```

Examples of invalid base 10 integer literals:

```c
int_invalid_leading_0 = 01013
int_invalid_all_0s = 00000
```


### Floating Point Literals

As the Imp language was initially implemented for the JVM, we use the Java IEEE floating point specification (a subset of the IEEE 754 standard).

Floating point variables are represented as decimals with an optional scientific notation exponent.

```c
float_lit_pi = 3.14159265
float_lit_plank = 6.62607015e-34
```

### String Literals

ToDo

### List Literals

ToDo




# Blocks

A block is a possibly empty sequence of statements within matching braces. Note that the upper level of an Imp program is not wrapped in matching braces, but still behaves as a block.

```g4
block : LBRACE statementList? RBRACE
```

Blocks influence scoping.

# Scope

ToDo


# Statements

Statements control execution of an Imp program.

```g4
statement
    : block
    | functionStatement
    | classStatement
    | returnStatement
    | ifStatement
    | loopStatement
    | expression
    | variableStatement
    | assignment
    | importStatement
    | exportStatement
    ;
```

## Function statements

A function declaration binds an indentifier, the function name, to a block of statements. Functions exist only in the current scope unless exported.

```g4
functionStatement
    : FUNCTION identifier LPAREN (arguments)? RPAREN (type)? block
    | LPAREN (arguments)? RPAREN FATARROW block
    ;
```
### Named functions

Functions are defined as follows:

```imp
function sum(x int, y int) int {
    return x + y
}

```

Each named function posesses a [Function Signature](todo), consisting of the function identifier, owner, return type, and argument types.

### Anonymous (lambda) functions

Todo.








## Return statements

Return statements terminate execution of the current function, optionally providing a result value.

```g4
returnStatement
    : RETURN (expression)?
    ;
```

Functions do not need an explicit return statement, but an empty return statement will be added by the compiler at the end of a function missing an explicit return. Unlike some languages (Ruby), the last expression is not returned by default.

The type of the expression returned by any return statements in the function must match any declared type of the function signature.

## If statement

Conditional execution of two branches.
Todo: add lisp-style switch/cond

# Semantics

## Function Signatures

Todo





# Definitions

Definitions that may be useful while reading this spec.
