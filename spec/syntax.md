The syntax of CCL is based upon the idea of S-Expressions. An S-Expression is 
either an atom or a list.

The process of turning source code into S-Expressions is known as *parsing*.

Source Code
-----------

The syntax of CCL is based on interpreting sequences of characters stored in 
bitstreams such as files or terminal input.

The character encoding of source code is UTF-8.

Comments
--------

Anything from a semicolon to the end of a line is treated as a comment and 
otherwise ignored.

Atoms
-----

Atoms are what you would consider to be basic data types. An atom is either a 
number, a symbol or a string.

* A number is either an integer or a real.
	- An integer is a sequence of digits.
	- A real number is two sequences of digits separated by a decimal point.
	- A number prefixed with a dash is negative. Otherwise it is positive.
* A string is a sequence of characters surrounded by double quotes.
	- Characters preceded by a backslash are escaped characters.
* A symbol is a sequence of characters that are not quotes, double quotes, 
  parentheses or whitespace and are not solely digits.

Lists
-----

A list is a basic container. It consists of a whitespace-separated sequence of 
atoms or lists enclosed in parentheses.

Forms
-----

S-Expressions that are programmatically meaningful are known as *forms*. There
are five kinds of form:

1. Atoms other than symbols are *constant forms*.
2. Symbols are *variable forms*.
3. Lists where the first member is `quote`, `if`, `lambda`, `set!`, `define`,
   `begin` or `define-syntax` are *intrinsic forms*.
4. Lists where the first member is a symbol that has been registered as derived
   syntax are *derived forms*.
5. The rest are procedure calls.

Most of these forms are examined in the [section on semantics](semantics.md).
The rest of this section discusses derived syntax.

Derived Syntax
--------------

Using `define-syntax` it is possible to extend the syntax of CCL.

    (define-syntax *name* *expander*)

Registers *expander* (a procedure) to be used to process forms that begin with 
*name* (a symbol). The expander should be a procedure that takes a single 
argument, the expression to be expanded, and should return a single value, the
result of that expansion.

CCL uses *hygeinic macros*. This means that by default variables introduced by
expanders do not shadow variables introduced by expressions that include derived
forms implemented by those expanders.

As an example, `let`, a binding form, may be implemented using `define-syntax`
like so:

    (define-syntax let
      (lambda (expr)
        (define vars (cadr expr))
        (define body (caddr expr))
        (cons (cons 'lambda (cons (map car vars) body))
              (map cadr vars))))
          
          
          
          
