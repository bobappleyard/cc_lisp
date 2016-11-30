Semantics
=========

CCL programs are sequences of S-Expressions. Executing a program consists of 
*evaluating* these forms in the order that they are encountered in the program.
A side-effect of this evaluation process is that useful work is performed by the
evaluator.

Evaluating some expressions will create definitions of things that may be used
later. Other expressions will perform work immediately upon evaluation. Others
still may schedule work to be performed in future.

Evaluation Order
----------------

With some exceptions, CCL expressions are evaluated as soon as they are 
encountered. Notably, arguments to a procedure are evaluated before the
procedure in question is activated.

The most notable exceptions are:

* `quote` witholds evaluation of expressions.
* `if` conditionally evaluates expressions.
* `lambda` delays evaluation of expressions.

[Derived syntax](syntax.md#derived-syntax) may use these in order to provide
sophisticated control over evaluation.

Scope
-----

Evaluation occurs with respect to a scope. A scope is a set of bindings. Each
binding associates a variable with a value. All variables that can be accessed
from a given location in a program are known as "in scope."

Scopes are nested. This nesting is organised lexically, which is to say 
according to the structure of the program. Expressions in a block will be able
to refer to all variables in that block and any blocks that the block appears
within. When a block has finished evaluation the variables in its associated 
scope can no longer be accessed. When this happens the variables are said to
have "gone out of scope."

When a procedure is defined, the scope it was defined in is stored along with
the procedure. This allows variables that would have otherwise gone out of scope
to be referred to.

Constant Values
---------------

Numbers and strings evaluate to themselves.

The symbols `true` and `false` evaluate to the boolean values `true` and `false`
respectively.

`quote` forms:

	(quote *datum*)

evaluate to the syntactic form of `datum`, i.e. withold evaluation.

Variables
---------

A variable gives a name to a value. Symbols are used to refer to variables.

Variables are introduced using [binding forms](lib.md#binding-forms). Chief 
amongst these is `define`, which introduces a binding into the enclosing scope.

	(define x 2)
	(print x)       ; prints 2
	(define (f) x)
	(print (f))     ; also prints 2

Conditional Evaluation
----------------------

Conditional forms enable the programmer to specify a choice of expression to
evaluate depending on the value of an expression.

The most basic of these is `if`:

    (if *cond* *then* *else*)
    
To evaluate `if`:

1. Evaluate *cond*.
2. If *cond* evaluates to `false`, the expression as a whole evaluates to 
   whatever *else* evaluates to.
3. Otherwise, the expression as a whole evaluates to whatever *then* evaluates
   to.

Other mechanisms for conditional evaluation are provided by 
[choice forms](lib.md#choice-forms).

Procedure Calls
---------------


