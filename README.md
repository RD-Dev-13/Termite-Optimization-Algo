# Termite-Inspired Swarm Intelligence for Optimization Problems



## Figures

The source refers to PDF figures with explicit figures/ paths. These seven files are required by main.tex and included in the Overleaf archive.

1. [itso_architecture.pdf](figures/itso_architecture.pdf) — flow of initialization, archive memory, queen-guided movement, stagnation-triggered alate dispersal, greedy replacement, restarts, and termination.
2. [convergence_sphere.pdf](figures/convergence_sphere.pdf) — mean best-so-far convergence for Sphere.
3. [convergence_rastrigin.pdf](figures/convergence_rastrigin.pdf) — mean best-so-far convergence for Rastrigin.
4. [convergence_rosenbrock.pdf](figures/convergence_rosenbrock.pdf) — mean best-so-far convergence for Rosenbrock.
5. [convergence_ackley.pdf](figures/convergence_ackley.pdf) — mean best-so-far convergence for Ackley.
6. [ablation_reconstructed.pdf](figures/ablation_reconstructed.pdf) — mean and standard deviation for the separate reconstructed, non-fixed-budget ablation experiment.
7. [main_adjusted_pvalues.pdf](figures/main_adjusted_pvalues.pdf) — Holm-adjusted p-values for ITSO versus PSO and GA on the main benchmark comparison.

The convergence curves aggregate the supplied run histories across 30 runs per algorithm and benchmark. Shaded regions show plus or minus one standard deviation across runs, not confidence intervals. The Sphere and Ackley plots use logarithmic fitness axes. The ablation visualization is specifically from the reconstructed, non-fixed-budget implementation; it is not the corrected fixed-budget experiment.

An additional [ablation_adjusted_pvalues.pdf](figures/ablation_adjusted_pvalues.pdf) is included for reference but is not used in the paper. The paper's ablation tests and table contain values recalculated from the raw reconstructed ablation records.

## Tables and result files

Key audit files in tables/:

- main_comparison.csv — per-benchmark, per-algorithm mean, standard deviation, minimum, maximum, and run count.
- main_statistics.csv — Friedman omnibus results and paired Wilcoxon comparisons of ITSO against each baseline, including raw and Holm-adjusted p-values.
- ablation_summary_recomputed.csv — descriptive results recalculated from the 480 run-level records for the reconstructed ablation.
- ablation_statistics_recomputed.csv — independent Mann–Whitney U tests for the reconstructed ablation, with Holm correction across 12 comparisons.
- fixed_budget_summary_corrected.csv — corrected fixed-budget summary as supplied in the corrected summary file, including descriptive fitness and evaluation-count statistics.

The .tex files in tables/ preserve generated table row extracts for review. The current main.tex embeds the table rows directly so the Overleaf project does not depend on those auxiliary files.

## Experimental data and implementation distinctions

The analysis used project materials found under the supplied Bio/ITSO_latest_research_results folder:

- main_experiment_results.csv
- results/full_convergence_histories.csv
- results/ablation_experimental_results.csv
- results/stage_c_corrected/corrected_summary.csv

The notebook contains multiple ITSO implementations. The paper distinguishes the original main comparison implementation, the alternative reconstructed ablation implementation, and the later corrected fixed-budget implementation. Their results are reported separately.

### Main comparison

- Four benchmark functions: Sphere, Rastrigin, Rosenbrock, and Ackley.
- Ten decision variables, population size 30, 300 maximum iterations, and 30 runs for each algorithm/function pair.
- The main runs use matching random seeds across algorithms. The notebook's initialization draws the same initial population for the corresponding benchmark and seed, so the main ITSO-versus-baseline comparisons use paired Wilcoxon signed-rank tests.
- Holm correction is applied across the eight ITSO-versus-PSO/GA post-hoc tests.
- Friedman omnibus tests are reported separately for each benchmark.
- Evaluation counts are not equal across algorithms. GA and PSO use 9,030 evaluations per run; ITSO uses additional evaluations during partial restarts and varies by run. The paper therefore does not describe the main comparison as equal-budget.

### Reconstructed, non-fixed-budget ablation

- The ablation experiment uses a separate reconstructed implementation with 30 runs per configuration and benchmark.
- It is not the exact main ITSO implementation and is not the corrected fixed-budget implementation.
- Since disabling a component changes subsequent random-number use, raw ablation outcomes are treated as independent samples. Mann–Whitney U tests and Holm correction across 12 comparisons are used.
- Recalculated results show corrected evidence of worse outcomes after removing memory on Ackley and Sphere, and after removing queen-driven growth on Ackley. Other mechanism/benchmark contrasts do not remain significant after correction.

### Corrected fixed-budget ablation

- The corrected summary reports 30 runs per configuration and benchmark, with a nominal budget of 9,150 evaluations.
- Corrected run-level observations were not included in the supplied files. The file named fixed_budget_ablation_runs.csv corresponds to preserved original Stage C results and disagrees materially with the corrected summary.
- Consequently, the paper reports the corrected summary descriptively and does not recompute independent-sample significance tests from the superseded run file.
- The supplied corrected paired-Wilcoxon output is not used for inferential claims because matching run indices do not establish valid pairing after configuration-specific random streams diverge.

## Scientific and reproducibility notes

- Reported numerical results come from supplied result files or are recalculated from supplied per-run observations. No corrected fixed-budget run values were inferred from summary statistics.
- Runtime hardware and exact Python/package versions were not recorded in the materials, so wall-clock times are not used as portable performance claims.
- The experiment covers four synthetic, ten-dimensional continuous benchmarks. It does not evaluate constrained engineering problems or real-world applications.
- The supplied bioinspired.pdf is an earlier conceptual manuscript that states that it contains no completed experiments. Its unverified placeholder reference was not reused.
- The paper does not claim overall ITSO superiority. The observed best mean differs by benchmark: PSO leads on Sphere and Ackley, GA on Rastrigin, and ITSO on Rosenbrock.



The source uses the IEEEtran conference class and keeps standard IEEE sizing and margins. Result tables are allowed to float within a column where possible, and a float barrier is placed before the Discussion so result figures and tables do not drift into the final discussion and references. The built-in editor compile succeeds. Check the final Overleaf PDF preview after upload to confirm that its page count and figure placement match your Overleaf compiler version.
