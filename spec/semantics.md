Semantics
=========

CCL programs are sequences of forms encoded in S-Expressions.

Constant Values
---------------

Numbers and strings evaluate to themselves.

`quote` forms:

	(quote **datum**)

evaluate to the syntactic form of `datum`, i.e. withold evaluation.

Variables
---------

A variable gives a name to a value. Symbols are used to refer to variables.

Variables are introduced using [binding forms](lib.md#binding-forms). Chief amongst these
is `define`, which introduces a binding into the enclosing scope.

	(define x 2)
	(define (f) x)

A variable exists within a scope. CCL is lexically scoped. That means that scopes are
nested according to where they appear in the source code of a program.

Conditional Evaluation
----------------------


