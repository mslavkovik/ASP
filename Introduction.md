# A basic introduction to answer set programming
## What are answer sets? 
To define answer sets we first must introduce Herbrand logic. Recall that to define a logic we need to define its syntax and its semantics. The syntax specifies what a well writen formula in the logic is. The semantics describes how the formulas in the logic are evaluated to a truth value (typically true or false). 
A logic is classical if its semantics uses two truth values: true and false. A logic is non-classical, also called multi-valued,  if its semantics uses more that two truth values. In addition to true and false, there can also be undecided, unknown, or even other values. 
## Herbrand logic
The syntax of Herbrand logic is the same as the syntax of first order logic. The elements of the syntax are: 
- variables
- predicate symbols (also called relation symbols) of arbitrary arity greater then 0
- function symbols of arbitrary arity
- constants (that are function symbols of arity 0)
- terms; recursivly defined 
