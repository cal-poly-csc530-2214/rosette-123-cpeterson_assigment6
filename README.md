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

I don't have a simple and fast way of verifying this solution, but I'm reasonably confident in the process that I took to reach it. It's definitely in CNF and I don't think I made any major logical missteps when simplifying it (although it's possible my best-guess Tseytin transformation was done incorrectly).
