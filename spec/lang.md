CCL is a simple Lisp similar to Scheme. What follows is a description of the syntax and semantics of CCL.

Syntax
======

The syntax of CCL is based upon the idea of S-Expressions. An S-Expression is either an atom or a list.

Source Code
-----------

The syntax of CCL is based on interpreting sequences of characters stored in bitstreams such as files or terminal input.

The character encoding of source code is UTF-8.

Atoms
-----

Atoms are what you would consider to be basic data types. An atom is either a number, a symbol or a string.

* A number is either an integer or a real.
	- An integer is a sequence of digits.
	- A real is two sequences of digits separated by a decimal point.
* A string is a sequence of characters surrounded by double quotes.
	- Characters preceded by a backslash are escaped characters.
* A symbol is a sequence of characters that are not quotes, double quotes, parentheses or whitespace and
  are not solely digits.

Lists
-----

A list is a basic container. It consists of a whitespace-separated sequence of atoms or lists enclosed in parentheses.

Semantics
=========

CCL programs are sequences of forms encoded in S-Expressions.

Constant Values
---------------

Numbers and strings evaluate to themselves.

`quote` forms:

	(quote **datum**)

evaluate to the syntactic form of `datum` (i.e. it witholds evaluation).

Variables
---------

A variable gives a name to a value. Symbols are used to refer to variables.

Variables are introduced using (binding forms)[lib.md#binding-forms]

A variable exists within a scope. CCL is lexically scoped. That means that scopes are
nested according to where they appear in the source code of a program.

