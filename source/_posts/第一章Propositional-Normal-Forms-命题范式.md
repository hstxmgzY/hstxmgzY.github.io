---
title: 第一章Propositional Normal Forms 命题范式
date: 2023-01-02 11:03:36
tags: 
	- 大二上
	- 离散数学
categories: 离散数学
description: 离散数学第一章笔记
---



本文参考[浙大计院的NCJ的离散数学详解 Discrete Mathematics Explained in Detail](https://github.com/iamNCJ/Discrete_Mathematics_Explained_in_Detail)，仅用于复习巩固

<font size=6> Chapter 01 Logic and Proofs 逻辑与证明</font>

Part 03

Normal Forms

------

# Propositional Normal Forms 命题范式

A **literal** is a variable or its negation.

> 变量及其否定统称为**文字**，如 $p$ 和 $\neg p$

Disjunctions (conjunctions) with one or more literals as disjuncts (conjuncts) are called **disjunctive (conjunctive) clauses**.  

> 由一个或多个文字所构成的析取（合取）式称作 **析取（合取）子句**

## Two Normal Forms 两类基本范式

### Disjunctive Normal Form 析取范式 DNF

A formula is said to be in disjunctive normal form if it is written as a disjunction, in which all the terms are conjunctions of literals.

> 由有限个简单**析取式的合取**构成的命题公式称为**析取范式**，形如 $(p\or q)\and(p\or q)$

### Conjunctive Normal Form 合取范式 CNF

A compound proposition is in Conjunctive Normal Form (CNF) if it is a conjunction of disjunctions.

> 由有限个简单**合取式的析取**构成的命题公式称为**合取范式**，形如 $(p \and q) \or (p \and q)$

## Identify Normal Forms 判定范式

|              p               | **DNF & CNF** |
| :--------------------------: | :-----------: |
|          **¬p ∨ q**          | **DNF & CNF** |
|       **¬p ∧ q ∧ ¬r**        | **DNF & CNF** |
|      **¬p ∨ (q ∧ ¬r)**       |    **DNF**    |
| **¬p ∧ (q ∨ ¬r) ∧ (¬q ∨ r)** |    **CNF**    |

The trick lies in that in some cases, clauses can be seen **as a whole**, and **as a DNF or CNF**.

## How to Obtain Normal Form 产生范式的方法

1. Faced with **→ & ↔**

   $p → q ≡ ¬p ∨ q$

   $p ↔ q ≡ (p → q) ∧ (q → p)$

2. Faced with **¬**

   $\neg(p_1\wedge p_2\wedge...\wedge p_n)\equiv\neg p_1\vee\neg p_2\vee...\vee\neg p_n$

   $¬¬p ≡ p$

3. Use of the commutative laws, the distributive laws and the associative laws to obtain normal form

[![pSM1b8I.md.png](https://s1.ax1x.com/2023/01/14/pSM1b8I.md.png)](https://imgse.com/i/pSM1b8I

## Full Disjunctive(Conjunctive) Normal Form 主析取（合取）范式

### Minterm and Maxterm 极小项、极大项

A **minterm** is a conjunctive of literals in which each variable is represented **exactly once**.

A **maxterm** is a disjunctive of literals in which each variable is represented **exactly once**.

> 在含有n个命题变量的简单合取式（简单析取式）中，若每个命题变量和它的否定恰好出现一个且仅出现一次，而且命题变量或它的否定式按下标从小到大或按字典序排列，称这样的简单合取式（简单析取式）为**极小项（极大项）**

### Full Disjunctive(Conjunctive) Normal Form 主析取（合取）范式

If a formula is expressed as **a disjunction of minterms**, it is said to be in **full disjunctive normal form**.

If a formula is expressed as **a conjunctive of maxterms**, it is said to be in **full conjunctive normal form**.

> 所有简单合取式（简单析取式）都是极小项（极大项）的析取范式（合取范式）称为主析取范式（主合取范式）

### [Important!] the Association Between Normal Forms and Truth Table （重点！）范式与真值表的关系

 #### DNF & Truth Table

[![pSM1LxP.md.png](https://s1.ax1x.com/2023/01/14/pSM1LxP.md.png)](https://imgse.com/i/pSM1LxP)

[![pSM1q2t.md.png](https://s1.ax1x.com/2023/01/14/pSM1q2t.md.png)](https://imgse.com/i/pSM1q2t)

The reason why this works:

1. Each minterm is true for exactly one assignment.
2. If A and B are two distinct minterms, then A ∧ B ≡ F.
3. A disjunction of minterms is true only if at least one of its constituents minterms is true.

#### CNF & Truth Table

[![pSM1XKf.md.png](https://s1.ax1x.com/2023/01/14/pSM1XKf.md.png)](https://imgse.com/i/pSM1XKf)

## Prenex Normal Form 前束范式

> Why we need it?
>
> - simplifies the surface structure of the sentence
> - useful to automated theorem proving

$$Q_1x_1Q_2x_2...Q_nx_nB$$

$$Q_i(i = 1,2,...,n)$$ is ∀ or ∃ and the formula B is **quantifier free**

**Any expression can be converted into prenex normal form.**

### How to obtain prenex normal form?

1. Eliminate all occurrences of → and ↔ from the formula in question.
2. Move all negations inward such that, in the end, negation only appear as part of literals.
3. Standardize the variables apart(when necessary).
4. The prenex normal form can now be obtained by moving all quantifiers to the front of the formula.

e.g.

[![pSM1vqS.md.png](https://s1.ax1x.com/2023/01/14/pSM1vqS.md.png)](https://imgse.com/i/pSM1vqS)
