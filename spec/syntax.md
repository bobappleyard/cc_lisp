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
	- A real number is two sequences of digits separated by a decimal point.
	- A number prefixed with a dash is negative. Otherwise it is positive.
* A string is a sequence of characters surrounded by double quotes.
	- Characters preceded by a backslash are escaped characters.
* A symbol is a sequence of characters that are not quotes, double quotes, parentheses or whitespace and
  are not solely digits.

Lists
-----

A list is a basic container. It consists of a whitespace-separated sequence of atoms or lists enclosed in parentheses.

Forms
-----

A list with a symbol as its first item is known as a form. 

* Most valid forms are procedure calls.
* A subset of forms are syntactic forms.

Core Forms
----------

It is possible to derive the rest of the language

	<core form> = (if <cond> <then> <else>?)
	            | (lambda (<var>...) <decl>...)
	            | (define <var> <expr>)
