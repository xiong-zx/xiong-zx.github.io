# Query access under heavy-tailed noise | Proof guide

Joint work of Zhixiao Xiong, Huiwen Jia, and Ying Cui. The formal statements and proofs below are pinned to [Lean v0.4.0][release], commit 09dfb3cbe13aca0f791bea3ecb34d1943ae61340. This guide gives the mathematical dependencies, then links to the full proof terms and derivations. Use the declaration signatures for exact hypotheses and constants.

## Model

Minimize a differentiable, bounded-below nonconvex objective F on R^d, with F(0) − inf F ≤ Δ. A query returns only the vector g(x, ξ). The sample ξ is hidden. At each fixed x, E g(x, ξ) = ∇F(x) and ‖g(x, ξ) − ∇F(x)‖ in L^p is at most σ. At every fixed pair x, y, the L^q norm of g(x, ξ) − g(y, ξ) is at most L̄‖x − y‖, using the same ξ at both points. At q = ∞ this is an almost-sure bound for each fixed pair. By Jensen, the increment condition gives an L̄-Lipschitz population gradient.

1. **Single:** Pick a decision from the past and private randomness, then obtain one gradient from a fresh independent sample.
2. **Paired:** Pick both decisions before drawing one fresh independent sample. Receive both gradients, at a cost of two evaluations.
3. **Reuse:** At each evaluation pick a decision and a sample handle using the history. Each distinct handle corresponds to an independent draw, and queries at an old handle use its original draw.

In all three protocols, the output may be a measurable point that was never queried. The budget is deterministic. Risk is E‖∇F(output)‖ over the samples and private randomness. The minimax budget must guarantee risk at most ε in every dimension. The dimension of a lower-bound instance may depend on the budget and problem parameters. Read the definitions in [Model][model] and the [paired and reuse contract][reuse-contract].

## Main statements

Let 1 < p ≤ 2, 1 ≤ q ≤ ∞, r = p/(p−1), S = max(1, σ/ε), A = L̄Δ/ε², and A ≥ 10,752,000. At q = ∞ set r/q = 0. Write N for the minimax evaluation budget and Θ for two-sided bounds with constants depending only on p and q.

| Protocol | Order of N | Checked declarations in HeavyTailedNoise.Matching |
| --- | --- | --- |
| Single | Θ(S^r + A S^max(2,r/q)) | [k1_matching][single], [k1_matching_inf][single-inf] |
| Paired and reuse | Θ(S^r + A S^max(1,r/q)) | [paired_reuse_matching and paired_reuse_matching_inf][paired] |

## Proof dependencies

1. **Reuse lower bound.** The one-dimensional pair of instances [NoiseReuse.lean][noise] gives the S^r contribution. The informativeness of a sample is rare, and on the all-zero transcript the two instances are indistinguishable. A separate sign-block chain, adapted from [Chen et al., §6.2][chen], forces the algorithm to make progress through successive hidden blocks. For the A S^(r/q) contribution, samples are rarely informative. For the A S contribution, each sample is only weakly informative about the signs. The construction verifies the moment and increment conditions for all fixed decisions.

   For a single stage, reveal the current block's record of a handle upon its first use in the comparison process. Conditional on the hidden block, a first reveal is drawn from the block distribution, and a repeat retrieves a known record. The KL bound charges first reveals and data processing transfers it to the observed record. Relate the reference probability of touching the block to the biased experiment using the stage event inequality. Prefix locality transfers the comparison to the actual oracle. See [LazyRevealLaw.lean][lazy], [StagePinhole.lean][pinhole], [TableKL.lean][kl], and the [reuse proof architecture][reuse-contract]. The noiseless case supplies the A contribution. Combining the branches gives the order S^r + A max(S,S^(r/q)).

2. **Single-query lower bound.** The reuse lower bound transfers to single queries. The additional A S² contribution uses a gated chain with randomly oriented directions and independent additive Gaussian noise. Its noise cancels from every same-sample difference, so the hard instance satisfies the increment bound even at q = ∞. The Gaussian information bound controls how quickly a fresh-query algorithm can identify successive directions. The construction also controls queries and outputs that touch later directions prematurely. See the [gated Haar proof dependencies][dependencies] and the [q = ∞ lower entry][gated-inf]. Together the two lower bounds give the single-query order.

3. **Single-query upper bound.** The method clips residuals about a coarse gradient tracker into layers and keeps a separate exponential average per layer. Fresh responses at a decision feed all layers. Bound the sum of their stochastic errors with the full same-sample kernel, retaining the dependence between layers. Separately control clipping bias, initial error, and drift of layer means. The expected average estimation error and normalized descent then give an output of risk at most ε. See the [single-query upper contract][single-upper] and its [proof dependencies][dependencies].

4. **Paired upper bound and matching.** Same-sample differences estimate the change in the mean while the remaining residual is clipped. Use single-memory clipped momentum variance reduction for q ≤ 2, and dyadic clipping layers for finite q ≥ 2. At q = ∞ apply the finite-q algorithm at q = r. See [U1Main.lean][u1] and [U2Main.lean][u2]. The risk-preserving embeddings in the [access model][model] give N_reuse ≤ N_paired and N_reuse ≤ N_single. The reuse lower bound and paired upper bound therefore sandwich both N_reuse and N_paired between constant multiples of the same rate.

## Check the formal statements

Check out [v0.4.0][release] with the Lean and mathlib versions pinned by the repository. Run the build and declaration/axiom audits from the [release notes][reproduce]. The [tagged CI run][ci] passed the build and all four audits. For which numerical constants and variant algorithms the package checks, see the [contracts][reuse-contract] and [release notes][reproduce].

[release]: https://github.com/xiong-zx/heavy-tailed-noise-lean/releases/tag/v0.4.0
[reproduce]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/docs/release-v0.4.0.md
[ci]: https://github.com/xiong-zx/heavy-tailed-noise-lean/actions/runs/40157117648
[model]: https://github.com/xiong-zx/heavy-tailed-noise-lean/tree/v0.4.0/HeavyTailedNoise/Model
[reuse-contract]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/docs/paired-reuse-contract.md
[single]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/HeavyTailedNoise/Matching/SingleRate.lean
[single-inf]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/HeavyTailedNoise/Matching/SingleInf.lean
[paired]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/HeavyTailedNoise/Matching/PairedReuse.lean
[noise]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/HeavyTailedNoise/Lower/Reuse/NoiseReuse.lean
[chen]: https://arxiv.org/abs/2610.16832v2
[lazy]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/HeavyTailedNoise/Lower/Reuse/LazyRevealLaw.lean
[pinhole]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/HeavyTailedNoise/Lower/Reuse/StagePinhole.lean
[kl]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/HeavyTailedNoise/Lower/Reuse/TableKL.lean
[gated-inf]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/HeavyTailedNoise/Lower/Gated/GatedHaarInf.lean
[dependencies]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/docs/proof-dependencies.md
[single-upper]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/docs/k1-upper-contract.md
[u1]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/HeavyTailedNoise/Upper/Paired/U1Main.lean
[u2]: https://github.com/xiong-zx/heavy-tailed-noise-lean/blob/v0.4.0/HeavyTailedNoise/Upper/Paired/U2Main.lean
