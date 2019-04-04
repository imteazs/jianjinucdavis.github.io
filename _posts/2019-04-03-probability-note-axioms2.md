---
layout: post
title: Probability Note Axioms
description: "Probability Axioms"
modified: 2019-04-01
comments: true
share: true
tags: [probability, learning_notes]
---

#### Probability Axioms

Axioms are the basis of modern mathematics. Axioms are basic properties that either does not need to prove or cannot be proved. The whole subject is based on the few axioms. Therefore it is very important to understand the axioms.

##### Axiom 1:
For any event A, P(A) >= 0;
##### Axiom 2:
P(S) = 1
Sample space is the universal set of all possible outcomes
##### Axiom 3:
For mutual exclusive A1, A2, … ==> P(A1 U A2 U … U An) = P(A1) + P(A2) + … + P(An)
Axiom 3 connects set operation with probability.

Holy tri-axioms of Probability

#### Properties of Probability

1. 
If E = {o1, o2, …, on}, and o1, o2, …, on are mutual exclusive
P(E) = P({o1}) + p({o2}) + … + P(on)

2. 
P({null}) = 0
S and {null} are mutual exclusive. AND S = S U {null}. P(S U {null}) = P(S) + P({null}) = P(S) = 1. Therefore P({null}) = 0

3.
P(A) = 1 - P(complement of A)
A and Ac are mutual exclusive; A U Ac = S
P(A U Ac) = P(A) + P(Ac) = P(S) = 1
P(A) = 1 - P(Ac)

4.
P(A) = P(A-B) + P(A intersects B)
A-B and A intersects B are mutual exclusive
A = (A-B) U (A intersects B)
P(A) = P((A-B) U (A intersects B)) = P(A-B) + P(A intersects B)

5.
P(A U B) = P(A) + P(B) - P(A intersects B)
AUB = (A - B) U (A intersects B) U (B - A)
P(AUB) = P((A - B) U (A intersects B) U (B - A)) = P(A-B) + P(A intersects B) + P(B-A) =  P(A) + P(B) - P(A intersects B)

6.
If C1, C2, …, Cn are mutual exclusive and C1 U C2 U … U Cn = S
For any event A, P(A) = P(A intersects C1) + P(A intersects C2) + … + P(A intersects Cn)
A Intersects S = A
A intersects (C1 U C2 U … U Cn) = (A intersects C1) U (A intersects C2) U … U (A intersects Cn)
Therefore, P(A) = P(A intersects S) = P(A intersects (C1 U C2 U … U Cn)) = P((A intersects C1) U (A intersects C2) U … U (A intersects Cn)) =  P(A intersects C1) + P(A intersects C2) + … + P(A intersects Cn)

7.
If A is a subset of B, P(A) < P(B)

8. Boole’s inequality
For n events A1, A2, …, An, P(Union of A1, A2, …, An) <= sum(P(Ai)) for i in n

9. Bonferroni inequality: http://www.cargalmathbooks.com/24%20Bonferroni%20Inequality.pdf


