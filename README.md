## Scripts and data associated with 'Avian flight accelerates genome evolution and shapes machineries for energy production'

1_cut_exons.Rscript - Run cut_exons to take the taxa selected for analyses from b10k c123 unfiltered data.
Requires
Code:
phangorn
Folder:
c123
File:
GreatAuk/OUT-0003_gff_aln-q30_razorbill_v2_sort9_clean_greatAuk.fa
locus_codes.csv

2_align_basic_iq.Rscript - Make initial macse alignment and tree.
Requires
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

3_clean_fast_tips.Rscript - Trim overly fast taxa. This assumes an exp distr of branch lengths where branches in the top 1% of the distribution are removed.
Selected loci saved to postshrink alignments - 14957 loci on latest count
Requires
Code:
MASS
phangorn
trimLongTipBrs.R
Folder:
basic_alignments

4_dnds_runs.Rscript - Run dnds_runs to run paml and erable to infer dn and ds trees.
Requires
Code:
phangorn
erable
dnds_template.ctl
Folder:
postshrink_alignments

5_dnds_collect.Rscript - Collect comparisons among sister pairs (of tips) as the proportion of length of one sister over another (avoiding the issue of absolute length, or age or rate differences among pairs). Branches were restricted to fall within realistic bounds. Small values have high variance, while high values are probably saturated (and probably poorly modelled).
Requires
Code:
phangorn
Folder:
dnds_analyses
postshrink_alignments

6_blast_loci.Rscript - Identify most likely locus function using BLASTN.
Requires
Code:
phangorn
Folder:
postshrink_alignments

7_id_focal_loci.Rscript - Identify the top and bottom percent of genes with a consistent difference in rate in sister pairs (less-flying over more-flying), excluding loci containing under 50% of the comparisons among sisters. The code includes each of four categories of vol-vol, nonvol-vol, sed-mig, and fles-vol.
Requires
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

8_prep_dating.Rscript - Collect the loci with low rtt.cov and non-extreme rates, leading to 313 loci, and concatenate them.
Requires
Code:
phangorn
rtt.cov.R
pathnode.R
concatenate.R
Folder:
postshrink_alignments

9_binomtests.Rscript - Assess each gene using binomial test for a signal of acceleration or decelarion in flightless taxa.
Requires
Code:
phangorn
Folder:
dnds_analyses
File:
dnds_sisdifs_vol.Rdata

10_genome_size.Rscript - Test for differences in a broad range of metrics of genome size among flightless and volant pairs.
Requires
Code:
phangorn
File:
Supplementary_Table_1_corrected.csv
taxonomy_codes.csv
GreatAuk/OUT-0003_gff_aln-q30_razorbill_v2_sort9_clean_greatAuk.fa

11_age_rate_acceleration.Rscript - Run regression models of how genome size and mutation rate are explained by flight.
Requires
Code:
phangorn
lavaan
Folder:

File:
dnds_sisdifs_vol.Rdata
taxon_comparisons_fless_flying.csv
taxonomy_codes.csv
dated.auk.tre

