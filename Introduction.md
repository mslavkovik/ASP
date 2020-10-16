# A basic introduction to answer set programming
## What are answer sets? 
Answer sets are stable models od a logic program. We explain first what logic programs are and then what stable models are.  

## Logic programs 
A logic program P is a set of logic rules. 

A logic rule r is a structure of the form

H<sub>1</sub> v ... v H <sub>m</sub> :- B<sub>1</sub>, ... , B <sub>k</sub>, not B<sub>k+1</sub>, ... , not B <sub>n</sub>.

Where H<sub>1</sub>, ..., H <sub>m</sub>, B<sub>1</sub>, .., B <sub>k</sub>, B<sub>k+1</sub>, . . .,B <sub>n</sub> are propositional literals or first order logic literals (atoms or strongly negated atoms). The symbol "v" denotes a disjunction. The symbol "," denotes a conjunction.  The symbol ":-" denotes inference. Strong negation is denoted with "-". The symbol "not" denotes weak negation, or negation as failure. The logic rule is read as follows: 
"Exactly one of H<sub>1</sub>, ..., H <sub>m</sub> is true when all of B<sub>1</sub>, .., B <sub>k</sub> are true and it cannot be proven that any of the B<sub>k+1</sub>, . . .,B <sub>n</sub> are true".

The part of the rule on the left handside of :- is called *the head* of the rule, while the part of the rule on the right handside of :- is called *the body* of the rule. We can write head(r)={H<sub>1</sub>, ..., H <sub>m</sub>} and body(r)={ B<sub>1</sub>, .., B <sub>k</sub>, B<sub>k+1</sub>, . . .,B <sub>n</sub>}.

A rule is called:
* a **fact** when n=0 and m=1,  namely when the body of the rule is empty and the head contains only one literal.
* a **disjuntive fact** when n=0 and m>1,namely when the body of the rule is empty and the head contains arbitrarily many literals.
* a **constraint** when m=0,n namely when the body of the rule is empty.
* a **positive rule**  when the n=k, namely when there are no weakly negated literals in the body of the rule.
* a **definitive rule**  when the m=1, namely when there is only one literal in the head of the rule.

A logic program P is called a **positive logic program** if all the rules in it are positive. 

## Minimal Herbrand model of a positive logic program 
Given a logic program P, the *Herbrand Universe* of P is the set of all ground terms formed using just the constants and function symbols in S. 

Consider for example the program 
p(1).
-q(2). 
p(y). 
r(f(x),x)}:- p(x),not q(x).

The *Herbrand Universe* for this prigram is the set {1,2,f(1),f(2),f(f(1)),f(f(2)), f(f(f(1))),...}.

Given a logic program P, the *Herbrand base* of P is the set of all ground literal Cθ where C is a  literal *occuring in the head* of some logic rule in P and θ assigns the variables in C to terms in the Herbrand universe.

The example logic program from above has as a  Herbrand base the following set: 

{1,2, p(1), -q(2), p(2), r(f(1),1), r(f(2),2), r(f(f(1)),1),r(f(f(2)),2), r(f(f(f(1))),1),...}.

The *grounding for a logic program P* is  the set of all ground rules rθ where r is a  logic rule in P and θ assigns the variables in r to terms in the Herbrand universe.

The example logic program from above has as grounding following set: 

{1,2, p(1), -q(2), p(2),r(f(1),1)}:- p(1), not q(1)., r(f(f(1)),f(1))}:- p(f(1)),not q(f(1)).,...}.


A Herbrand interpretation for a positive logic program P is a subset of the Herbrand base of P. 

A Herbrand interpretation I is a model for a logic rule r if:
- each of the literals B<sub>1</sub>, .., B <sub>k</sub> unifies with at least one literal in I
- at least one of the literals H<sub>1</sub>, .., H <sub>m</sub> unifies with a literal in I

A Herbrand interpretation I is a **minimal herbrand model for a logic rule r** if it is a model for r and it does not have a proper subset that is a model for r. 


A **minimal Herbrand model for a positive logic program P** is a Herbrand interpretation for P that is a minimal herbrand model for each of the logic rules in P. 

Consider the following logic program P: 

p(1).
-q(2). 
p(y). 
r(x,x) v -r(x,x):- p(x), q(x).

The Herbrand universe of P is {1,2}. The Herbrand base of P is {p(1),-q(2),p(2),r(1,1),-r(1,1), r(2,2), -r(2,2)}

I={p(1), -q(2), p(2)} is a minimal Herbrand model for P, while I={p(1), -q(2), p(2),-r(1,1)} is not a minimal Herbrand model for P although it is a model for P.

Consider the following logic program P: 

p(1).
-q(2). 
p(x). 
r(x,x) v -r(x,x):- p(x).

The Herbrand universe of P is {1,2}. The Herbrand base of P is {p(1),-q(2),p(2),r(1,1),-r(1,1), r(2,2), -r(2,2)}
This logic program has four minimal Herbrand models: 
* I={p(1), -q(2), p(2),r(1,1)}  
* I={p(1), -q(2), p(2),-r(1,1)} 
* I={p(1), -q(2), p(2),r(2,2)}  
* I={p(1), -q(2), p(2),-r(2,2)} 


## Reduct of a logic program 

Consider a logic program P and a set M that is a subset of the literals that occur in P. A reduct of P with respect to M, denoted P<sup>M</sup> is a logic program obtained from P by: 
1. Deleting all the rules that contain not B in the body, where B is an element of M 
2. Deleting all the remaining literals not B' from the bodies of all the remaining rules in P 

## Stable models of a logic programs

A set M is a stable model of a logic program P if it is one of the minimal Herbrand models of P<sup>M</sup>. 

A set M is an answer set of a logic program P if it is a stable set of P. 

## Examples

Program:

p(1,2).
q(x):- p(x,y), not q(y).

has one stable model M={p(1,2), q(1)}.

Program:

p:- not p.

has no stable models.

Program:

p:- -p.

has one stable models M=Ø.


Program: 

p:- not q.
q:-not p.

has two stable models M={p} and M={q}.

Program:

-p.
p:- -q

has one stable model M={-p}.

Program:

-p.
q:- -p

has one stable model M={-p,q}.

Program:

 p v q.
r:-not q.

has two stable models M={p,r} and M={q}.



