# Complexity
*Pages 17-XX*

Multiple qualifications identify classes of problems based on time complexity; many problems are related 
in some abstract way and can be reduced from one to another.

Three main complexity classes:
* Simple, rather boring problems can be solved in a short amount of time; 
what a mathematician would call *P* time.
* More difficult problems, such as a group of people trying to decide on the optimal location for a pint 
and some food, are more complex and solvable in exponential time, or *exp*
* Some problems are so complex that they can’t be solved in all the time we can possibly have (R, or “finite time” -- 
making these problems *beyond R*), and are simply undecidable. For instance: Turing’s Halting Problem

There are special subclasses of problems that are of great interest to us, specifically: exponentially 
complex problems that we can solve in P time with a nondeterministic lucky guess. These problems are in a 
classification called *NP*. We can further divide this complexity class into decision problems that we can
quickly verify (*NP-Complete*) and more complicated problems that are in *exp*, but that other problems in NP
can be reduced to in P time (*NP-Hard*).

Deterministic system: execute a routine and obtain a result. Based on that result, execute another routine
for another result, and so forth. Results link together until answer obtained.

Non-deterministic system: execute a routine and obtain a result. Execute one of a series of next steps:
exactly which is decided at that time. Once whatever that step is has been executed, again execute one of
a series of next steps, again without knowing which until it's chosen. At least from a deterministic program's
point of view, there is no way to determine how we got to our answer. Lucky process. 

If a problem is:
* solvable in exp
* verifiable in P
* also solvable in P by non-deterministic methods

It is classifiable in non-deterministic polynomial (NP) time. NP is a somewhat mythical time frame, 
since we don't know whether a non-deterministic algorithm is possible. 

This is quite common--one version of a problem classified differently than its decision problem reduction. 
Decision problems are almost always NP-Complete because the answer to the problem can be verified, while 
combinatorial problems are NP-Hard. 

##### ELI5: P, NP, NP-Hard, NP-Complete
*https://www.reddit.com/r/explainlikeimfive/comments/t3fp4/eli5_np_completeness/c4j7rsj/*
* **P:** The set of all problems that can be solved in polynomial time (polynomial in relation to the input) 
by a deterministic Turing machine.
* **NP:** The set of all problems that can be solved in polynomial time if you have a non-deterministic 
Turing machine. That is, if you have a magical computer that can perform both actions at a decision point 
simultaneously. However, given a proposed solution to a problem in NP, that solution can be verified in 
polynomial time by a normal, deterministic Turing machine.
* **NP-hard:** The set of all problems that any problem in NP can be reduced to in polynomial time.
* **NP-complete:** The set of problems that any problem in NP can be reduced to in polynomial time, 
whose solutions can still be verified in polynomial time. This is the subset of NP-hard that overlaps NP. 
Generally-speaking, the set of NP-complete problems is a kind of "upper bound" on the complexity of NP 
problems. Every NP problem can be solved by an NP-complete problem, and the solution can be verified in 
polynomial time.

Turing's *Halting Problem* is beyond R, meaning solvable only with an infinite amount of time. It is 
however (possible to reduce to?) a simple decision problem: will this program halt? Because of that, other 
problems in NP can be reduced to it, earning it the classification NP-hard.

The *Cook-Levin Theorem* (Leonid Levin & Stephen Cook, early 1970s): any problem in NP can be reduced to
The Boolean Satisfiability Problem (SAT):
> ...the problem of determining if there exists an interpretation that satisfies a given Boolean formula.
> In other words, it asks whether the variables of a given Boolean formula can be consistently replaced by
> the values `true` and `false` in such a way that the formula evalutes to `true`. 

```java 
if ((x && y) && (x && !y) || ((x || y) && (x || !y)) {
//...
```
SAT wants to know what values for `x` and `y` will return `true`.

##### Richard Karp, 1972 -- *Reducibility Among Combinatorial Problems*
> https://en.wikipedia.org/wiki/Karp%27s_21_NP-complete_problems*

A number of NP problems can be reduced to NP in polynomial time; *Karp's 21 NP-Complete Problems*. Taking a 
look at a few:

**Knapsack**
Around for over 100 years, this is a combinatorial optimization problem centering on packing a bag for the
weekend. 

> Given a set of items, each with a weight and a value, determine the number of each item to include in a
> collection so that the total weight is less than or equal to a given limit and the total value is as large
> as possible.

tl; dr optimize combination of price and weight for limited space.

**Clique**
Formulated in 1935 and relating to graphs and graph theory:

> Consider a social network, where the graph's vertices represent people, and the graph's edge represent
> mutual acquaintance. Then a clique represents a subset of people who all know each other, and algorithms
> for finding cliques can be used to discover these groups of mutual friends. 

The solution to this problem could apply to any social aspect of an application, or grouping of things
like "things" that are self-assembling. 

**Bin Packing**
A variation of Knapsack:

>...objects of different volumes must be packed into a finite number of bins or containers each of volume
>V in a way that minimizes the number of bins used. 

NP-Hard problem. A combinatorial optimization problem. verifying that things have been packed 
optimally requires carrying out every possible iteration to prove that ours is the best. Can be reduced to 
a decision problem by iterating over bin configurations and asking whether the current configuration is
optimal, and this reduction would classify it as NP-complete. 

**Travelling Salesman**
Find the cheapest way to send a salesman on a trip:

>Given a list of cities and the distances between each pair of cities, what is the shortest possible route
>that visits each city exactly once and returns to the origin city?

NP-Hard problem. Can be reduced in *P* time to an NP-Complete decision problem by enumerating through every
valid path and asking "Is there a shorter path?"

##### Approximations and Laziness
There exists algorithms which in some cases "solve" some of these problems in *P* time; these are called
approximations and are useful if their inexact nature can be tolerated.