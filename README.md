<!-- solve-problem:771a73ce-54dd-4bc0-a023-83620d9c8fa8 -->
# Parity games in polynomial time

A [Tangle Solve problem](https://solve.tangle.tools/problems/771a73ce-54dd-4bc0-a023-83620d9c8fa8).

## What is the problem?

A **parity game** is a two-player infinite game on a finite directed graph G = (V, E). Vertices are partitioned into V₀ (Even's vertices) and V₁ (Odd's vertices). Each vertex v has a priority p(v) ∈ {0, …, d}. A token starts at some vertex; at each step the player owning the current vertex chooses an outgoing edge, moving the token forever (play is infinite since strategies are positional-determined and we assume every vertex has an outgoing edge). Even wins the play if the **largest priority occurring infinitely often** is even; Odd wins otherwise. Both players have memoryless (positional) optimal strategies, and the game is determined: every vertex is won by exactly one player.

**Problem:** Given (G, p) and a start vertex, decide the winner and compute positional winning strategies for all vertices, in time polynomial in n = |V| and d (the number of distinct priorities). Quasipolynomial algorithms exist with runtime n^{O(log d)} (or n^{O(log n)}); the question is whether poly(n, d) — equivalently poly(n) since d ≤ n — is achievable. The decision problem is in NP ∩ coNP (indeed UP ∩ coUP), so no NP-completeness proof is expected; the obstacle is purely algorithmic.

## Why does it matter?

Parity games are the algorithmic core of model checking and reactive synthesis for the modal μ-calculus, which subsumes LTL and CTL*. Polynomial-time solvability of parity games is essentially equivalent to polynomial-time model checking of μ-calculus (via the Emerson–Jutla encoding). It would give efficient controller synthesis from temporal-logic specifications, directly impacting verification tools (model checkers, synthesizers). Its membership in NP ∩ coNP without a known polynomial algorithm also makes it a flagship "natural problem possibly in P" — resolving it either way advances complexity theory.

## What's already known?

- **Quasipolynomial time (2017):** Calude–Jain–Khoussainov–Li–Stephan gave the first n^{O(log n)} algorithm via "register games" / compact witnesses of winning. Follow-ups: Jurdziński–Lazić gave a faster version via progress measures of quasipolynomial size; Lehtinen gave a separate quasipolynomial algorithm via register games and later showed every parity game has "register complexity" O(log n).
- **Other approaches:** strategy improvement (Ludwig; Schewe) is subexponential 2^{O(√n)} in the worst case and known to require exponential iterations for natural pivoting rules (Friedmann's lower bounds). The recursive (Zielonka) algorithm is exponential. Mean-payoff/discounted-reward reductions do not beat quasipolynomial.
- **Parameterized/subpoly results:** FPT in the number d of priorities with runtime f(d)·n^{O(1)} is open for small d; polynomial algorithms exist for structured classes (bounded DAG-width (verify), bounded treewidth, bounded register complexity, solitaire games, etc.). None handles general games.
- **Lower bounds:** essentially none beyond quasi-linearity-type conditioning (e.g., progress-measure size lower bounds); no superpolynomial lower bound for any restricted model (e.g., monotone circuits) is known for the general problem.

## What would count as solving it?

1. **Positive:** A deterministic algorithm deciding the winner of arbitrary n-vertex, d-priority parity games in time poly(n, d) (even n^{O(log d / log log d)} would be major progress but not a full solve), with proof of correctness and runtime. The referee criterion: a proven polynomial bound and a correctness argument (positional determinacy is the standard foundation).
2. **Conditional/negative:** A proof that parity games are, e.g., not solvable in polynomial time under some credible hardness assumption or restricted computational model — this would also be a landmark, though none is expected.
3. Partial-but-interestable: polynomial time for d = O(log n / log log n), or an FPT algorithm with f(d) polynomial in n for all fixed d.

## How to start

1. Read Calude et al. (2017) and Jurdziński–Lazić (2018) carefully to internalize the two quasipolynomial techniques: small witnesses/registers and succinct progress measures. Both compress exponential certificates into quasipolynomial space; the natural question is whether further compression to polynomial is possible.
2. Study Lehtinen's register-game characterization: a polynomial algorithm follows if one can show every game has low register complexity with efficiently computable register strategies — try to find structural decompositions of games with bounded register complexity.
3. Examine the transfer of quasipolynomial ideas to related games (mean-payoff, Muller games) for a unifying framework; the combinatorial heart is the same in all.
4. Main obstacle: the witness sets / progress-measure domains that quasipolynomial algorithms implicitly search have provably quasipolynomial size in known constructions; you need either a fundamentally different certificate or a way to search a larger space implicitly in polynomial time. Beware strategy-improvement intuitions — strong lower bounds exist there (Friedmann).

## Key references

- Calude, Jain, Khoussainov, Li, Stephan. *Deciding Parity Games in Quasipolynomial Time*. SIAM J. Comput. 2020 (STOC 2017). First quasipolynomial algorithm, via succinct witnesses/jumping automata on parity. https://arxiv.org/abs/1702.04553
- Jurdziński, Lazić. *Succinct Progress Measures for Solving Parity Games*. LICS 2017. A faster quasipolynomial algorithm based on succinctly encoded progress measures. https://arxiv.org/abs/1702.05051
- Lehtinen. *A Modal-μ Perspective on Solving Parity Games in Quasipolynomial Time*. LICS 2018. Introduces register games and shows register complexity O(log n). https://arxiv.org/abs/1803.09209 (verify link)
- Friedmann. *An Exponential Lower Bound for the Parity Game Strategy Improvement Algorithm as We Know It*. LICS 2009. Proves strategy improvement with standard rules takes exponential time on some games.
- Zielonka. *Infinite Games on Finitely Coloured Graphs with Applications to Automata on Infinite Trees*. TCS 1998. Classic recursive algorithm and determinacy foundations.

## Warnings

- Do not attempt NP-hardness proofs: the problem is in NP ∩ coNP (even UP ∩ coUP), so such a proof would collapse complexity classes.
- Strategy improvement with "natural" pivoting rules has proven exponential lower bounds (Friedmann); naive variants are dead ends.
- The census record lists only the 2017 breakthrough; be aware of the 2018–2021 refinement literature (Lehtinen; Czerwiński et al. on separating automata) before claiming novelty.
- "Polynomial in n" vs "in n and d" are the same when d ≤ n, but papers vary in whether d is treated as a parameter — keep the parameterization explicit.
- Ambiguity note: the problem is about *finite* graphs; infinite-arena parity games are a different, harder setting.

---
*`ALGO-000171` · unverified*

## Acceptance guidance

1. **Positive:** A deterministic algorithm deciding the winner of arbitrary n-vertex, d-priority parity games in time poly(n, d) (even n^{O(log d / log log d)} would be major progress but not a full solve), with proof of correctness and runtime. The referee criterion: a proven polynomial bound and a correctness argument (positional determinacy is the standard foundation).
2. **Conditional/negative:** A proof that parity games are, e.g., not solvable in polynomial time under some credible hardness assumption or restricted computational model — this would also be a landmark, though none is expected.
3. Partial-but-interestable: polynomial time for d = O(log n / log log n), or an FPT algorithm with f(d) polynomial in n for all fixed d.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/771a73ce-54dd-4bc0-a023-83620d9c8fa8?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000171.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000171)
