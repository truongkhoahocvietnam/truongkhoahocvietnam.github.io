---
title: "Some linearization techniques in linear programming"
layout: post
date: 2021-12-04
permalink: /posts/2021/12/notes-linearization/ 
read_time: false
categories:
  - blog
header:
  teaser: /assets/post_materials/lp.png
tags:
  - linearization
  - linear program
---


Linear programming (LP) is the minimization of a linear form on a polyhedron[^Dantzig1955]. The standard form of an LP is

$$
\begin{align*}
\min & \quad c^\top x \\
     & \quad Ax = b, \\
     & \quad x \geq 0,
\end{align*}
$$

where $$c \in \mathbb{R}^n$$, $$b \in \mathbb{R}^m$$, and $$A$$ is the $$m{\times}n$$-matrix of coefficients. LP has been shown[^Liberti2018] to be fell into the computational complexity class **P**. It is hard sometimes to cast the problem as an LP. It such situation we may need to add some integer or binary variables. This leads us to an MILP (mixed integer LP) problem, which includes ILP (integer variables only), BLP (binary variables only), or LP as a special case. MILP is another fundamental problem in mathematical programming, and has been shown to be **NP**-hard[^Liberti2018].  


[^Dantzig1955]: G. Dantzig, A. Orden, and P. Wolfe. The generalized simplex method for minimizing a linear form under linear inequality restraints. *Pacific Journal of Mathematics*, 5(2):183–196, 1955.

[^Liberti2018]: L. Liberti, Mathematical Programming. *Lecture Notes*, Ecole Polytechnique, 2018.


## Some linearization techniques
Following are some linearization techniques which transform nonlinear terms to linear forms, which may involve additional (usually integer or binary) variables.

##### 1. Max-min functions
The term $$X = \max\{x_{1}, x_{2}\}$$ can be linearized by introducing an additional binary decision variable $$y$$ and using the so-called big-$$M$$ method.

The following constraints[^SE_max] enforce the definition of $$X$$ and $$y$$:

$$
\begin{align*}
X & \geq x_{1}, \\
X & \geq x_{2}, \\
X & \leq x_{1} + M(1 - y), \\
X & \leq x_{2} + My.
\end{align*}
$$   

Similarly, the term $$X = \min\{x_{1}, x_{2}\}$$ can be linearized as follows[^SE_min]

$$
\begin{align*}
X & \leq x_{1}, \\
X & \leq x_{2}, \\
X & \geq x_{1} - M(1 - y), \\
X & \geq x_{2} - My.
\end{align*}
$$ 

The value of $$M$$ has to be carefully chosen. See more [here](https://or.stackexchange.com/questions/236/why-is-it-important-to-choose-big-m-carefully-and-what-are-the-consequences-of-d).

[^SE_max]: StackExchange, [*How to formulate (linearize) a maximum function in a constraint?*](https://or.stackexchange.com/questions/711/how-to-formulate-linearize-a-maximum-function-in-a-constraint/712#712). Accessed Dec. 2021.

[^SE_min]: StackExchange, [*How to linearize min function as a constraint?*](https://or.stackexchange.com/questions/1160/how-to-linearize-min-function-as-a-constraint). Accessed Dec. 2021.


##### 2. Rounding functions: Ceil and Floor

A floor function $$y = \lfloor x \rfloor$$ can be linearized as[^SE_round]


$$
\begin{align*}
& x - 0.999 \leq y \leq x, \\
& y \in \mathbb{Z_+}. 
\end{align*}
$$

Similarly, a ceiling function $$y = \lceil x \rceil$$ can be linearized as

$$
\begin{align*}
& x \leq y \leq x + 0.999, \\
& y \in \mathbb{Z_+}. 
\end{align*}
$$

[^SE_round]: StackExchange, [*Linear program with ceiling or floor functions*](https://math.stackexchange.com/questions/1862885/linear-program-with-ceiling-or-floor-functions). Accessed Dec. 2021.


##### 3. Product of two binary variables
A product term $$x_{1}x_{2}$$, where $$x_{1}, x_{2} \in \{0,1\}$$ occuring in a linear program can be replaced by an auxiliary continuous variable $$y \in [0,1]$$ and the following so-called Fortet' constraints[^Fortet1960]:

$$
\begin{align*}
y & \leq x_{1}, \\
y & \leq x_{2}, \\
y & \geq x_{1} + x_{2} - 1.
\end{align*}
$$

[^Fortet1960]: R. Fortet. Applications de l’algèbre de Boole en recherche opérationelle. *Revue Française de Recherche Opérationelle*, 4:17–26, 1960.


##### 4. Product of multiple binary variables
The above technique could also be extended to the product of multiple variables: $$y_\mathcal{I} = \prod_{i \in \mathcal{I}} x_i$$, where $$x_i \in \{0,1\}$$, $$\forall i \in \mathcal{I}$$. The linearization constraints are[^Liberti2018]

$$
\begin{align*}
y_{\mathcal{I}} & \leq x_{i}, \quad \forall i \in \mathcal{I}, \\
y_{\mathcal{I}} & \geq \sum_{i \in \mathcal{I}} x_{i} - |\mathcal{I}| + 1.
\end{align*}
$$

##### 5. Product of a binary and a non-negative continuous variable

Suppose we have a binary variable $$x \in \{0,1\}$$ and a non-negative continuous variable $$y \in \mathbb{R_+}$$. The product $$z = xy$$ is thus

$$
z=\begin{cases}
0 & \text{if }x=0, \\
y & \text{if }x=1.
\end{cases}
$$

$$z$$ can be linearized by using the big-$$M$$ method[^SE_prod],

$$
z \geq y - (1-x)M,
$$

where $$z \in \mathbb{R_+}$$, $$M$$ is a sufficiently large value so that it would not be part of any feasible solution.

[^SE_prod]: StackExchange, [*How to linearize the product of a binary and a non-negative continuous variable?*](https://or.stackexchange.com/questions/39/how-to-linearize-the-product-of-a-binary-and-a-non-negative-continuous-variable). Accessed Dec. 2021.


##### 6. Activate or deactivate a specific constraint

The Big-$$M$$ method can also be used to activate or deactivate a specific constraint as follows[^SE_activate]

* **LEQ (less-than-or-equal-to) constraint** (i.e., $$Ax \leq b$$): It could be activated/deactivated by using an additional variable $$y  \in \{0,1\}$$ as
  
  $$
  Ax \leq b + M(1 − y).
  $$
  
  Here if $$y = 0$$ the constraint $$Ax \leq b$$ is deactivated, and otherwise if $$y = 1$$.
   
* **GEQ (greater-than-or-equal-to) constraint** (i.e., $$Ax \geq b$$): Then we need the following
  
  $$
  Ax \geq b − M(1−y).
  $$

  If all coefficients in $$A$$ are nonnegative, we can instead write
  
  $$
  Ax \geq b(1−y),
  $$
  
  which is tighter than the previous constraint.
   
* **Equality constraint** (i.e., $$Ax = b$$): Then the following constraints are used
  
  $$
  \begin{align*}
   Ax & \leq b + M(1 − y), \\
   Ax & \geq b − M(1 − y)
  \end{align*}
  $$

[^SE_activate]: StackExchange, [*In an integer program, how can I “activate” a constraint only if a decision variable has a certain value?*](https://or.stackexchange.com/questions/76/in-an-integer-program-how-can-i-activate-a-constraint-only-if-a-decision-vari). Accessed Sept. 2023.

##### 7. Preventing loops in linear directed graph
Let $$x_{ij}$$ be a binary variable indicating that the arc $$(i,j)$$ is present, the constraint

$$
\sum_{i,j\in\mathcal{V}^{'}}x_{ij}\leq\left|\mathcal{V}^{'}\right|-1,\quad\forall\mathcal{V}^{'}\subseteq\mathcal{V}
$$

will prevent creating loops in a linear directed graph[^Cycle_Elimination].

[^Cycle_Elimination]: StackExchange, [*Cycle elimination constraint in a directed graph*](https://math.stackexchange.com/questions/2479079/cycle-elimination-constraint-in-a-directed-graph). Accessed Feb. 2024.


See more:
* How to specify an IF-THEN constraint with an Integer Linear Programming (ILP) solver: [1](https://yzuda.org/Useful_Links/optimization/if-then-else-01.html), [2](https://yzuda.org/Useful_Links/optimization/if-then-else-01.html)
* [How to specify an unequal constraint with an Integer Linear Programming (ILP) solver](https://yzuda.org/Useful_Links/optimization/unequal.html)
* [In an integer program, how I can force a binary variable to equal 1 if some condition holds?](https://or.stackexchange.com/questions/33/in-an-integer-program-how-i-can-force-a-binary-variable-to-equal-1-if-some-cond)

  
### References

