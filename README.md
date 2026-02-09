## Scripts and data associated with 'Avian flight accelerates genome evolution and shapes machineries for energy production'

* 1_cut_exons.Rscript - Run cut_exons to take the taxa selected for analyses from b10k c123 unfiltered data.
	*	Requires
Code:
phangorn
Folder:
c123
File:
GreatAuk/OUT-0003_gff_aln-q30_razorbill_v2_sort9_clean_greatAuk.fa
locus_codes.csv

* 2_align_basic_iq.Rscript - Make initial macse alignment and tree.
	* Requires
Code:
phangorn
trimCols.R
trimCodons.R
macse_v2.03
iq-tree_v1.7
Folder:
exon_als_cut_auk
File:
trawk.tre

* 3_clean_fast_tips.Rscript - Trim overly fast taxa. This assumes an exp distr of branch lengths where branches in the top 1% of the distribution are removed.
Selected loci saved to postshrink alignments - 14957 loci on latest count
	* Requires
Code:
MASS
phangorn
trimLongTipBrs.R
Folder:
basic_alignments

* 4_dnds_runs.Rscript - Run dnds_runs to run paml and erable to infer dn and ds trees.
	* Requires
Code:
phangorn
erable
dnds_template.ctl
Folder:
postshrink_alignments

* 5_dnds_collect.Rscript - Collect comparisons among sister pairs (of tips) as the proportion of length of one sister over another (avoiding the issue of absolute length, or age or rate differences among pairs). Branches were restricted to fall within realistic bounds. Small values have high variance, while high values are probably saturated (and probably poorly modelled).
	* Requires
Code:
phangorn
Folder:
dnds_analyses
postshrink_alignments

* 6_blast_loci.Rscript - Identify most likely locus function using BLASTN.
	* Requires
Code:
phangorn
Folder:
postshrink_alignments

* 7_id_focal_loci.Rscript - Identify the top and bottom percent of genes with a consistent difference in rate in sister pairs (less-flying over more-flying), excluding loci containing under 50% of the comparisons among sisters. The code includes each of four categories of vol-vol, nonvol-vol, sed-mig, and fles-vol.
	* Requires
Code:
phangorn
ggplot2
reshape2
Folder:
dnds_analyses
blastSearches
File:
goterms.csv
dnds_branches.Rdata

* 8_prep_dating.Rscript - Collect the loci with low rtt.cov and non-extreme rates, leading to 313 loci, and concatenate them.
	* Requires
Code:
phangorn
rtt.cov.R
pathnode.R
concatenate.R
Folder:
postshrink_alignments

* 9_binomtests.Rscript - Assess each gene using binomial test for a signal of acceleration or decelarion in flightless taxa.
	* Requires
Code:
phangorn
Folder:
dnds_analyses
File:
dnds_sisdifs_vol.Rdata

* 10_aitchison_variance.Rscript - Calculate Aitchison variance (CLR-transformed base composition heterogeneity) for each alignment to quantify compositional heterogeneity across taxa per gene.
	* Requires
Code:
ape
Folder:
c123
Output:
aitchison_variance_results.csv
aitchison_variance_results.rds

* 11_base_composition_vs_rates.Rscript - Test whether Aitchison variance per gene correlates with Bernoulli test p-values from script 9. Confirms base composition heterogeneity is not confounding the evolutionary rate signal.
	* Requires
Code:
ggplot2
gridExtra
File:
p_values_per_locus.Rdata
aitchison_variance_results.csv

* 12_ks_permutation_envelopes.Rscript - Permutation-based calibration of KS tests from script 9. Shuffles flight-category labels across the 42 sister pairs (1000 permutations), recomputes per-gene binomial p-values, and builds pointwise 95% null CDF envelopes. Accounts for p-value discreteness with small N, gene-gene correlation, and fixed study design.
	* Requires
Code:
ggplot2
File:
dnds_sisdifs_vol.Rdata
p_values_per_locus.Rdata

* 13_genome_size.Rscript - Test for differences in a broad range of metrics of genome size among flightless and volant pairs.
	* Requires
Code:
phangorn
File:
Supplementary_Table_1_corrected.csv
taxonomy_codes.csv
GreatAuk/OUT-0003_gff_aln-q30_razorbill_v2_sort9_clean_greatAuk.fa

* 14_age_rate_acceleration.Rscript - Run regression models of how genome size and mutation rate are explained by flight. Frequentist path analysis with lavaan.
	* Requires
Code:
phangorn
lavaan
File:
dnds_sisdifs_vol.Rdata
taxon_comparisons_fless_flying.csv
taxonomy_codes.csv
dated.auk.tre
genomic_comparisons_data.csv
sheard_martin_traits.csv

* 15_bayesian_path_analysis.Rscript - Bayesian structural equation modelling of the same 7 competing path models from script 14, fitted with blavaan. Uses BUSCO completeness as an explicit assembly-quality covariate. Includes convergence diagnostics, model comparison (WAIC, LOO-IC), posterior predictive checks, and sensitivity analysis excluding the ATLROG-HELFUL outlier.
	* Requires
Code:
blavaan
lavaan
File:
dnds_sisdifs_vol.Rdata
taxon_comparisons_fless_flying.csv
taxonomy_codes.csv
dated.auk.tre
genomic_comparisons_data.csv
sheard_martin_traits.csv

* 16_plot_bayesian_results.Rscript - Publication figures for the Bayesian path analysis. Loads saved results from script 15 without re-fitting models.
	* Requires
Code:
blavaan
lavaan
ggplot2
File:
bayesian_path_results.Rdata
bayesian_path_sensitivity.Rdata

