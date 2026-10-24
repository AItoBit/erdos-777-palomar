# Erdős Problem 777: comparable pairs in set families

This repository packages an existing complete Lean proof of the three
Daykin–Erdős questions. Their answers, in order, are **yes, no, yes**.
It includes the entire substantive proof, adapted from
[plby/lean-proofs at commit 8822f7d](https://github.com/plby/lean-proofs/blob/8822f7ddef30fadbd92e1c6ab4ed897af356af5e/src/latest/ErdosProblems/Erdos777.lean).
No mathematical or formalization novelty is claimed. See NOTICE for attribution.

## The exact result

Let F be a family of m distinct subsets of an n-element set. Let E be the
number of unordered pairs of distinct members comparable by inclusion.

1. For every epsilon > 0, there is n0 such that for every n >= n0 and every
   F, if m <= (2-epsilon) 2^(n/2), then E < 2^n.
2. It is false that for every c > 0 there is C > 0 such that for every n
   and F, E >= c m^2 implies m <= C 2^(n/2).
3. For every epsilon > 0 there is delta > 0 such that for every n and F,
   E > m^(2-delta) implies m < (2+epsilon)^(n/2).

All divisions n/2 in these statements are real division. There is no parity
restriction. The third assertion covers every dimension, not only large n.
The formal theorem `Erdos777.erdos_777` states their conjunction explicitly.
These are extremal set theory results about density in the Boolean lattice,
relevant to researchers studying comparable pairs and extremal graph bounds.

## Proof account

For question 1, finite chain moments show that comparable triangles have
asymptotically vanishing density. Triangle removal and Mantel's theorem then
give E <= (1/4+eta)m^2. The coefficient becomes less than 1 after substituting
the hypothesis m <= (2-epsilon)2^(n/2) and choosing eta sufficiently small.
Smaller families and boundary values of epsilon are handled separately.

For question 2, take disjoint blocks X and Y of size r and an extra point z.
Use the lower sets A union {x}, for A subset X and x in Y, and upper sets
(X minus {y}) union B union {z}, for y in X and B subset Y.
The family has n=2r+1 and m=2r*2^r, with at least m^2/16 comparable pairs.
The ratio m/2^(n/2)=sqrt(2)r is unbounded. Thus c=1/16 supplies the
counterexample density.

For question 3, count a member B and t-tuples of members contained in B,
splitting according to the size of the tuple's union. A power-mean estimate
yields, for integers t >= 1,

    E^t <= m^t 2^n 2^(t floor(n/2)) + m^(2t-1) 2^floor(n/2).

Choosing t large and delta small proves the contrapositive in large
dimension. A separate finite-dimensional argument handles all small n and
empty families. None of these combinatorial results is an unproved
literature assumption; the development proves the needed bounds using Mathlib.

## Reproduction and trust

The project pins Lean 4.35.0-rc2 and Mathlib commit
`065356127b1dc0016f66b7283ce0ce2c4055aa55`.

```sh
lake update
lake exe cache get
lake build
lake env lean Solution.lean
```

`Challenge.lean` contains the same complete proof in compact formatting to satisfy
the submission line limit and the submitter's requirement of no proof holes
anywhere. The statement of record is the explicit theorem at its end.
`Solution.lean` preserves readable formatting of the full proof. `comparator.json`
selects the theorem and allows only `propext`, `Classical.choice`, and
`Quot.sound`. Comparator must verify the matching theorem types and permitted
axioms; Palomar additionally performs its own mechanical and editorial checks.

The original, unported source was compiled with Lean/Mathlib 4.33.1 and
reported only those three axioms. That check does not establish that this
port or a later commit passes. Check current build and Comparator evidence
for the exact submitted commit. No Palomar registration or NanoDa pass is
claimed in advance.

## Provenance and review

The [problem discussion](https://www.erdosproblems.com/forum/thread/777)
supplies the three questions. Mathematical context includes Alon–Frankl,
*The maximum number of disjoint pairs in a family of subsets* (1985),
and Alon–Das–Glebov–Sudakov, *Comparable pairs in families of sets* (2015).
Full links and source roles are recorded in `formalization.yaml`.

The original source credits Codex and GPT-5.6 Sol for the formalization.
The submission port and documentation were prepared with Codex assistance.
AItoBit is the responsible human account for this submission and packaging;
the submitter confirmed responsibility for the underlying formalization.
An agent performed a separate source-fidelity audit; no human peer review or
endorsement by the cited mathematicians is claimed. See `FIDELITY.md`.

The repository contains the complete adapted proof rather than depending on
the upstream proof repository. Apache-2.0 applies to this repository's code
and documentation; cited papers retain their own rights.
