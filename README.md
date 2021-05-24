# rosette-123-cpeterson_assigment6
rosette-123-cpeterson_assigment6 created by GitHub Classroom

## Question 2

Question 2 looked fairly daunting, but doable. This took a little over an hour since I wasn't familiar with Tseytin transformation and my prepositional logic was rusty.

The problem asks us to use Tseytin transformation to get an equisatisfiable CNF version of the following:

¬(¬r → ¬(p ∧ q))

I used the following auxilery variables:
- **a<sub>1</sub> ⟺ p ∧ q**
- **a<sub>2</sub> ⟺ ¬r → ¬a<sub>1</sub>**

Conjuncting all the substitutions:

¬a<sub>2</sub> ∧ (a<sub>2</sub> ⟺ ¬r → ¬a<sub>1</sub>) ∧ (a<sub>1</sub> ⟺ p ∧ q)

Replacing the ⟺s:

¬a<sub>2</sub> ∧ (a<sub>2</sub> → (¬r → ¬a<sub>1</sub>)) ∧ ((¬r → ¬a<sub>1</sub>) → a<sub>2</sub>) ∧ (a<sub>1</sub> → (p ∧ q)) ∧ ((p ∧ q) → a<sub>1</sub>)

Replacing the →s in the inner part of the expression:

¬a<sub>2</sub> ∧ (a<sub>2</sub> → (r ∨ ¬a<sub>1</sub>)) ∧ ((r ∨ ¬a<sub>1</sub>) → a<sub>2</sub>) ∧ (a<sub>1</sub> → (p ∧ q)) ∧ ((p ∧ q) → a<sub>1</sub>)

Replacing the rest of the →s:

¬a<sub>2</sub> ∧ (¬a<sub>2</sub> ∨ r ∨ ¬a<sub>1</sub>) ∧ (¬(r ∨ ¬a<sub>1</sub>) ∨ a<sub>2</sub>) ∧ (¬a<sub>1</sub> ∨ (p ∧ q)) ∧ (¬(p ∧ q) ∨ a<sub>1</sub>)

Working on the (¬(r ∨ ¬a<sub>1</sub>) ∨ a<sub>2</sub>) term, which becomes (¬r ∨ a<sub>2</sub>) ∧ (a<sub>1</sub> ∨ a<sub>2</sub>) after Demorgan's and distributing:

¬a<sub>2</sub> ∧ (¬a<sub>2</sub> ∨ r ∨ ¬a<sub>1</sub>) ∧ ((¬r ∧ a<sub>1</sub>) ∨ a<sub>2</sub>) ∧ (¬a<sub>1</sub> ∨ (p ∧ q)) ∧ (¬(p ∧ q) ∨ a<sub>1</sub>)

¬a<sub>2</sub> ∧ (¬a<sub>2</sub> ∨ r ∨ ¬a<sub>1</sub>) ∧ (¬r ∨ a<sub>2</sub>) ∧ (a<sub>1</sub> ∨ a<sub>2</sub>) ∧ (¬a<sub>1</sub> ∨ (p ∧ q)) ∧ (¬(p ∧ q) ∨ a<sub>1</sub>)

Then the (¬a<sub>1</sub> ∨ (p ∧ q)) term, which becomes (¬a<sub>1</sub> ∨ p) ∧ (¬a<sub>1</sub> ∨ q) after distributing:

¬a<sub>2</sub> ∧ (¬a<sub>2</sub> ∨ r ∨ ¬a<sub>1</sub>) ∧ (¬r ∨ a<sub>2</sub>) ∧ (a<sub>1</sub> ∨ a<sub>2</sub>) ∧ (¬a<sub>1</sub> ∨ p) ∧ (¬a<sub>1</sub> ∨ q) ∧ (¬(p ∧ q) ∨ a<sub>1</sub>)

Lastly, the (¬(p ∧ q) ∨ a<sub>1</sub>), which becomes (¬p ∨ ¬q ∨ a<sub>1</sub>) after Demorgan's:

**¬a<sub>2</sub> ∧ (¬a<sub>2</sub> ∨ r ∨ ¬a<sub>1</sub>) ∧ (¬r ∨ a<sub>2</sub>) ∧ (a<sub>1</sub> ∨ a<sub>2</sub>) ∧ (¬a<sub>1</sub> ∨ p) ∧ (¬a<sub>1</sub> ∨ q) ∧ (¬p ∨ ¬q ∨ a<sub>1</sub>)**

I don't have a simple and fast way of verifying this solution, but I'm reasonably confident in the process that I took to reach it. It's definitely in CNF and I don't think I made any major logical missteps when simplifying it (although it's possible my best-guess Tseytin transformation was done incorrectly). I thought this was a fun problem to work through and I learned quite a bit (as well as refreshed my boolean logic).

## Question 5

Question 5 looked doable. It took me around 10 minutes to set up CaDiCaL and produce ``cadical_output.txt`` using Cygwin. It took me around another hour to learn about CDCL, understand & parse the log file, and produce this writeup. For the sake of time, I'm going to describe the algorithm's process informally instead of the explicit writeup and implication graph mentioned in the homework.

The log file starts off with:
```
c LOG 0 checking that all clauses contain a negative literal
c LOG 0 found purely positively irredundant size 2 clause[3] 1 3
c LOG 0 checking that all clauses contain a positive literal
c LOG 0 found purely negatively irredundant size 2 clause[5] -4 -2
```
This step wasn't mentioned on any CDCL explanation I saw, and I'm honestly not sure what it's checking for and/or doing.

The log file then goes into the first guess, that x<sub>1</sub> = True. I don't understand what the watch/unwatch statements are doing, so I'll ignore those:
```
c LOG 0 checking increasing variable index true assignment
c LOG 1 search decide 1
c LOG 1 search assign 1 @ 1 decision
c LOG 1 propagating 1
c LOG 1 unwatch -1 in irredundant size 3 clause[1] -1 2 4
c LOG 1 watch 4 blit -1 in irredundant size 3 clause[1] 2 4 -1
c LOG 1 unwatch -1 in irredundant size 3 clause[7] -4 -1 2
c LOG 1 watch 2 blit -1 in irredundant size 3 clause[7] -4 2 -1
c LOG 1 search assign 3 @ 1 irredundant size 2 clause[9] 3 -1
c LOG 1 propagating 3
c LOG 1 unwatch -3 in irredundant size 3 clause[11] -3 -2 4
c LOG 1 watch 4 blit -3 in irredundant size 3 clause[11] -2 4 -3
c LOG 2 search decide 2
c LOG 2 search assign 2 @ 2 decision
c LOG 2 propagating 2
c LOG 2 search assign -4 @ 2 irredundant size 2 clause[5] -4 -2
c LOG 2 ignoring lucky conflict irredundant size 3 clause[11] -2 4 -3
c LOG 2 backtracking to decision level 0 with decision 0 and trail 0
c LOG 2 unassign 1 @ 1
c LOG 2 unassign 3 @ 1
c LOG 2 unassign 2 @ 2
c LOG 2 unassign -4 @ 2
c LOG 2 unassigned 4 literals 100%
c LOG 2 reassigned 0 literals 0%
```
It's clear that x<sub>3</sub> = True due to the (x<sub>3</sub> ∨ ¬x<sub>1</sub>) clause. This would add (x<sub>1</sub> = 1) → (x<sub>3</sub> = 1) to the implication graph.

The solver then guessed that x<sub>2</sub> = True. This meant that x<sub>4</sub> = False due to the (¬x<sub>4</sub> ∨ ¬x<sub>2</sub>) clause. This would add (x<sub>2</sub> = 1) → (x<sub>4</sub> = 0) to the implication graph.

These assignments led to a contradition, as the (¬x<sub>3</sub> ∨ ¬x<sub>2</sub> ∨ x<sub>4</sub>) clause is no longer satisfiable. This causes the solver to backtrack all the way to the start.

The solver then tries **x<sub>1</sub> = False**:
```
c LOG 0 checking increasing variable index false assignment
c LOG 1 search decide -1
c LOG 1 search assign -1 @ 1 decision
c LOG 1 propagating -1
c LOG 1 search assign 3 @ 1 irredundant size 2 clause[3] 1 3
c LOG 1 search assign 4 @ 1 irredundant size 2 clause[13] 1 4
c LOG 1 search assign -2 @ 1 irredundant size 2 clause[15] -2 1
c LOG 1 propagating 3
c LOG 1 propagating 4
c LOG 1 propagating -2
```
The solver finds that **x<sub>3</sub> = True** due to the (x<sub>1</sub> ∨ x<sub>3</sub>) clause. This would add (x<sub>1</sub> = 0) → (x<sub>3</sub> = 1) to the implication graph.

The solver then finds that **x<sub>4</sub> = True** due to the (x<sub>1</sub> ∨ x<sub>4</sub>) clause. This would add (x<sub>1</sub> = 0) → (x<sub>4</sub> = 1) to the implication graph.

Lastly, the solver finds that **x<sub>2</sub> = False** due to the (¬x<sub>2</sub> ∨ x<sub>1</sub>) clause. This would add (x<sub>1</sub> = 0) → (x<sub>2</sub> = 0) to the implication graph.

These assignments do not produce a contradiction and are taken as the proof that the problem is satisfiable. Overall, I enjoyed walking through this process and learning the mechanics behind boolean satisfiability solvers. I think it's interesting that the solvers operate on a (vastly optimized) guess-and-check framework.

## Question 6

The rest of the problems seemed to rely on Question 6. This problem took me around an hour to figure out, with the time evenly spent across the problems.

Github's markdown isn't the best, but I'll be using the variable p<sub>v</sub><sup>c</sup> to represent color(v) = c.
1. A single vertex being colored could be represented as an OR of it being each of k colors: (p<sub>1</sub><sup>1</sup> ∨ p<sub>1</sub><sup>2</sup> ∨ ... ∨ p<sub>1</sub><sup>k</sup>). These can be AND'd together n times to make sure each vertex has at least one color.
2. Two vertexes being different colors could be represented by (¬p<sub>u</sub><sup>a</sup> ∨ ¬p<sub>u</sub><sup>b</sup>), AND'd together for every vertex u in V and every pair of colors a, b (where a and b aren't the same) in C.
3. Both vertexes being the different colors would be represented by (¬p<sub>w</sub><sup>c</sup> ∨ ¬p<sub>v</sub><sup>c</sup>), AND'd together for every edge (v, w) pair in E and every color c in C.
4. From a purely satisfiability perspective, I think the limit on colors per vertex is unnecessary. Multi-coloring a vertex purely makes the problem harder (could just single color it any of the chosen colors instead). Therefore, we do not need to enforce it using constraints, as an optimal solution will just avoid the optional multi-coloring when it is necessary to do so, not changing the satisfiability at all.
5. My constraints are already in CNF. The first one uses |V|k variables and |V| clauses. The third one uses 2|E|k variables and |E|k clauses. Together, they use |V|k + 2|E|k variables and |V| + |E|k clauses.

I'm not sure these are all correct (particularily part #5), but I think I have the general idea correct. This was a fun problem to think about, especially part #4.

## Question 8

I spent around another hour thinking about Question 8, as it was the next logical step up from Question 6. I couldn't come up with an answer, but I had some interesting ideas which may have materialized into an answer with more time or more knowledge about the k-coloring problem.

I mostly thought about the second part of this problem: reducing the edge variables and clauses to |E|log(k). This felt somewhat possible, where the base of the logarithm might be related to the average connectivity of the graph, and the relationship would more directly model the fact that all connections from a vertex v must have a different color than v. I considered something along the lines of:

p<sub>v</sub><sup>c</sup> → ¬(p<sub>1</sub><sup>c</sup> ∨ p<sub>2</sub><sup>c</sup> ∨ ... ∨ p<sub>w</sub><sup>c</sup>)

Which basically says that if a node is a certain color, all of its neighboring nodes must be different colors. While this is a bit smarter, it doesn't avoid the fundamental issue of having to check the condition for every single color in the graph.

Ultimately, I suspect that the answer lies with more pre-determined color choices. I think that instead of giving every vertex an abitrary color (0, 1, 2, ..., k), you could give a vertex the lowest number possible. This would reduce the number of times colors must be checked and potentially hit the log(k) goal.

Overall, this problem was very interesting to think about and try ideas for, even if I didn't get too far. I'd be interested to see the solution.

## Conclusion and Future Work

I'm happy with my solutions, and felt as though I learned a decent amount. With more time, I think I would have been able to complete most of these problems, particularily the ones requiring Racket and the deeper dive into k-coloring, which were both too time prohibitive for me to really get into in 4 hours.
