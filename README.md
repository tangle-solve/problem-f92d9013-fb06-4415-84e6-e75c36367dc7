<!-- solve-problem:f92d9013-fb06-4415-84e6-e75c36367dc7 -->
# EFX for arbitrarily many agents with bi-valued chores

A [Tangle Solve problem](https://solve.tangle.tools/problems/f92d9013-fb06-4415-84e6-e75c36367dc7).

## What is the problem?

**Setting:** Fair division of *chores* (indivisible items, each agent dislikes every item she gets). There are $n$ agents and $m$ indivisible chores. Each agent $i$ has a cost function $c_i: \{1,\dots,m\}\to \mathbb{R}_{\ge 0}$ that is **additive**: $c_i(S)=\sum_{j\in S} c_i(j)$. An instance is **bi-valued (for chores)** if for each agent $i$ there are two values $a_i < b_i$ (often normalized so each cost is one of $\{a_i, b_i\}$; a common special case is all agents sharing values $\{1,2\}$) such that every chore has cost $a_i$ or $b_i$ under $i$.

An allocation $A=(A_1,\dots,A_n)$ partitions (here: fully allocates) the chores among agents. $A$ is **EFX** (envy-free up to any item) if for all agents $i,k$ and every chore $j\in A_i$:
$$c_i(A_i \setminus \{j\}) \le c_i(A_k).$$
That is, $i$'s envy toward $k$ vanishes after removing any single chore from $i$'s own bundle.

**Question (ALGO-000184):** Does every complete EFX allocation exist for every bi-valued additive chore instance, for **arbitrarily many agents** $n$? Known for $n\le 4$ (He–Tao); open for $n \ge 5$.

Ambiguity note: variants differ on whether the pair $\{a_i,b_i\}$ is agent-specific or global, and whether $a_i$ may equal $0$. The He–Tao result is for the per-agent bi-valued model; confirm exact model when reading the paper.

## Why does it matter?

EFX is the gold-standard fairness notion for indivisible items; it is famously open even for three agents with goods, and for chores general additive EFX has now been shown *not to exist* (per the census). Bi-valued valuations are the natural tractable boundary, and resolving this problem would map exactly where chore fairness collapses: a positive answer yields a clean algorithmic guarantee applicable to labor/task allocation with coarse (e.g., binary or tiered) cost scales; a negative answer would show bi-valuedness does not save EFX, sharpening the frontier of fair-division impossibility.

## What's already known?

- **General additive chores:** EFX allocations do not always exist (He–Tao 2026 report nonexistence; earlier, casting chores as negative goods does not preserve EFX because of how removal interacts with envy direction — verify exact construction). Pareto-optimality incompatibilities are also established.
- **Bi-valued goods:** positive results are known — EFX exists for bi-valued goods with arbitrarily many agents (e.g., work following Amanatidis et al. on few valuations / bivalued instances — verify citations independently).
- **Bi-valued chores, He–Tao (2026):** prove EFX existence for $n \le 4$ agents. Their technique presumably combines a small-$n$ case analysis with an exchange/adjustment argument; the barrier is that chore EFX breaks the monotone "give away the worst item" intuition that works for goods, and exchange cycles can create new envy.
- Lower/upper bound gap: existence known for $n\le4$, unknown (or false, unverified) for $n\ge5$. No hardness results specific to bi-valued chores EFX are recorded.

## What would count as solving it?

1. **Positive resolution:** a proof (ideally a polynomial-time algorithm) that every bi-valued additive chore instance admits a complete EFX allocation, for all $n$. Referee criterion: full existence theorem plus correct EFX verification argument; constructive algorithm strengthens it.
2. **Negative resolution:** an explicit bi-valued chore instance (with $n\ge5$) and a proof that no complete EFX allocation exists.
3. **Partial:** existence for $n=5$, or for the restricted global-$\{1,2\}$ valuation model, or a stronger structural characterization (e.g., EFX + PO coexistence).

## How to start

1. Read He–Tao (arXiv:2606.08872) closely: their 4-agent proof and their nonexistence construction for general valuations. The bottleneck case analysis will reveal which configurations fail to extend to 5 agents.
2. Try the global $\{1,2\}$ model first (all agents value chores as 1 or 2): search via exhaustive computer enumeration for 5-agent counterexamples; if none exist at small $m$, look for an invariant (e.g., a potential function on exchanges) enabling an induction on $n$ or $m$.
3. Attempt to port the bi-valued *goods* EFX algorithms (which do scale in $n$) via the chores-to-goods transformation $v_i = -c_i$; identify precisely which step fails — the EFX condition for costs requires envy to vanish when *removing a chore from the envier's bundle*, a different quantifier structure.
4. Main obstacle: envy in chores is "positive-cost envy," and standard tools (cut-and-choose, envy-graph cycles, scalings) were built for goods.

## Key references

- He, Ruihao (?) and Tao, Biaoshuai (?) (2026), *EFX for Additive Chores: Nonexistence, Pareto Incompatibility, and Bi-Valued Existence*, arXiv:2606.08872 — proves EFX may fail for general additive chores but exists for bi-valued instances with up to four agents. (Author names/details verify — the census gives only the arXiv ID.) https://arxiv.org/abs/2606.08872
- (Background, verify) Amanatidis, Birmpas, Christodoulou, Markakis — work on EFX and few valuation classes for goods, the standard comparison point for bi-valued existence results.
- (Background, verify) Caragiannis et al., *The Unreasonable Fairness of Maximum Nash Welfare* — defines EFX (for goods) and motivates the notion.

## Warnings

- The direction of the EFX quantifier for chores (envier removes from her own bundle) is easy to get backwards; double-check any reduction from goods techniques.
- Nonexistence for general additive chores (He–Tao) means naive attempts cannot work; any algorithm must exploit bi-valuedness.
- The census is 2026-dated and secondary; independently verify the He–Tao results, exact model (per-agent vs. global value pairs, zero allowed), and current status before building on them.

---
*`ALGO-000184` · unverified*

## Acceptance guidance

1. **Positive resolution:** a proof (ideally a polynomial-time algorithm) that every bi-valued additive chore instance admits a complete EFX allocation, for all $n$. Referee criterion: full existence theorem plus correct EFX verification argument; constructive algorithm strengthens it.
2. **Negative resolution:** an explicit bi-valued chore instance (with $n\ge5$) and a proof that no complete EFX allocation exists.
3. **Partial:** existence for $n=5$, or for the restricted global-$\{1,2\}$ valuation model, or a stronger structural characterization (e.g., EFX + PO coexistence).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/f92d9013-fb06-4415-84e6-e75c36367dc7?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000184.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000184)
