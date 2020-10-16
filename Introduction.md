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
- connectives and Parentheses: ¬, →, ↔, ∧, ∨, ( and )
- quantifiers: ∀(universal) and ∃ (existential);

The arguments of predicates and functions are terms. A term is recursivelly defined by two rules, being:
1. Every variable and constant is a term.
2. if $f$ is a function of arity m and $t_1,...t_m$ are terms, then $f(t_1,...,t_m)$ is also a term.

To introduce the semantics of Herbrand logic, we need to intorduce two concepts: Herbrand Universe and Herbrand Base. 

Given a set of Herbrand logic (or first order logic) formulas S in conjunctive normal form, the *Herbrand Universe* of S is the set of all ground terms formed using just the constants and function symbols in S. 

Consider for example the set 
S= { p(1), q(2), p(y), r(f(x),x)}

The Herbrand Universe for S is U={1,2,f(1),f(2),f(f(1)),f(f(2)), f(f(f(1))),...}

The *Herbrand base* of S is the set of all ground clauses Cθ where C ∈ S and θ assigns the variables in C to terms in the Herbrand universe.

For the example S= { p(1), q(2), p(y), r(f(x),x)}, the Herbrand base is the set 
B={1,2,p(1), q(2), p(2), r(f(1),1), r(f(2),2), r(f(f(1)),1),r(f(f(2)),2), r(f(f(f(1))),1),...}
