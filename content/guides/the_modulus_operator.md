---
title: "The Infamous modulus operator"
date: 2023-09-10
draft: false
summary: "a brief look at the modulus operator"
tags: ["modulus", "remainder", "programming"]
---

### Modulus? Remainder?
> What is the modulus operation? How is it different from remainder operation?

#### Euclidean Remainder

Mathematically, the remainder operation generally refers to _the Euclidean
division_ and the subsequent remainder of that operation. In Euclidean
division, the remainder will always be zero or positive. Let's have a
simplified example. Consider a dividend a of 27 and a divisor n of 4. 27 then
divided by 4 would then give a quotient q of 6 and a remainder r of 3.

This looks straight forward and simple. However things get a bit tricky when
one of either divisor or dividend or even both have negative integers
_(especially with respect to how they are implemented in different programming
languages)_.

Let us extend it to negative numbers, without using too much technical or in
this case mathematical jargons:

-  positive dividend & negative divisor :

take 27 divided by -4
given euclidean division, this should give q = -6 and r = 3 

- negative dividend & positive divisor :

take -27 divided by 4
given euclidean division, this should give q = -7 and r = 1

- negative dividend & negative divisor :

take -27 divided by -4
given euclidean division, this should give q = 7 and r = 1 

#### Modulo operation

> In mathematics, the result of the modulo operation is an equivalence class,
> and any member of the class may be chosen as representative; however, the
> usual representative is the least positive residue, the smallest non-negative
> integer that belongs to that class (i.e., the remainder of the Euclidean
> division). However, other conventions are possible. Computers and calculators
> have various ways of storing and representing numbers; thus their definition
> of the modulo operation depends on the programming language or the underlying
> hardware.
> 
> Modulo is a mathematical jargon that was introduced into mathematics in the
> book Disquisitiones Arithmeticae by Carl Friedrich Gauss in 1801. Given the
> integers a, b and n, the expression "a ≡ b (mod n)", pronounced "a is
> congruent to b modulo n", means that a − b is an integer multiple of n, or
> equivalently, a and b both share the same remainder when divided by n. It is
> the Latin ablative of modulus, which itself means "a small measure." The term
> has gained many meanings over the years—some exact and some imprecise.
> 
> [ Wikipedia]

As it turns out, modulo operation in fact represents an equivalence class,
depending on different definitions implemented in computing. The different
_definitions_ that could be used are:

- division with _truncation_ (which drops the decimal part generally)
- division with _floor function_ (which floors down)
- division with _ceiling function_ (which floors up generally)
- _euclidean division_ (which we looked at just now) 

All this said, let us now have a look at how these operations are performed in
programming languages. Every programming language has its own implementation of
the modulus operator, which has us, the users to know how the operation is
implemented in the languages we use.

Python for instance implements division with _floor function_ while Ocaml
implements division with _truncation_. I'll be linking resources at the bottom
of this article as to why these specific implementations are chosen. In brief,
a lot of it has to do with _[rounding](https://floating-point-gui.de/errors/rounding/), [floating point arithmetic](https://floating-point-gui.de/)
discrepancy in computing_ I might write an article explaining these topics later. 

While it can be confusing, it is our duty as _responsible programmers_ to
understand these differences and know why they are implemented this way, so
that we don't get surprised when we see them. _With that said, have a great
day._

#### References

- [Euclidean division](https://en.wikipedia.org/wiki/Euclidean_division)
- [Modulo with regards to computing](https://en.wikipedia.org/wiki/Modulo)
- [Modulo in mathematics](https://en.wikipedia.org/wiki/Modulo_(mathematics))
- [Python rounding](https://realpython.com/python-rounding/)
- [Guido Van Rossum on why floored division in python](https://python-history.blogspot.com/2010/08/why-pythons-integer-division-floors.html)
- [Helpful stack overflow discussion regarding this topic](https://stackoverflow.com/questions/24848789/why-does-pythons-modulus-operator-not-match-the-euclidean-definition)
- [Euclidean remainder calculator online](https://ezcalc.me/remainder-calculator/)
- [Modulo calculator online (Euclidean based)](https://ezcalc.me/modulo-calculator/)
