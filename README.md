This dataset provides 77 family level pHMMs describing RNA viral RdRps, which can be used for sensitive detection of sequences derived from viral RdRp in RNA sequence data.


## Background Information
Profile Hidden Markov Models (pHMMs) provide a more sensitive method than BLASTP for finding distant homologues of known protein sequences while (in contrast to structure-based approaches) maintaining computational speed (Eddy, 2011). We used known RNA virus sequences to develop 77 family-level RdRp pHMMs. 

## Directory Structure
#### alignments
Aligned, Stockholm format files of amino acid sequences used to create the pHMMs.

#### pHMMs
Profile HMMs created with HMMER (Eddy, 2011) to represent the alignments.

## Materials and Methods
### Construction of RNA dependent RNA polymerase pHMMs
Initially we used RNA virus groups and sequences from the “GRAViTy” analysis of Aiewsakun and Simmonds (2018). In cases where there was only a small number of sequences in a family-like group, or where some more recently published groups of viruses were not mentioned in Aiewsakun and Simmonds, we searched the NCBI taxonomy and nucleotide databases (April 2018) for additional reference sequences in order to make more representative pHMMs. In total, we used 1,793 RdRp protein and RdRp-containing polyprotein sequences to create 77 pHMMs.

Because many RdRps are contained within longer polyproteins, we wished to trim sequences to a core RdRp region. Therefore, we aligned the sequences within each group with MUSCLE v3.8.31 (Edgar, 2004) and compared the alignments using HHpred (Zimmermann et al., 2018) with the Pfam and PDB databases (Berman et al., 2000; Finn et al., 2014). Based on the second best matching RdRp (to avoid overfitting if the best match Pfam pHMM contained sequences from the same group), we cropped each alignment from both ends. Where appropriate, the alignments and coordinates for trimming were manually curated based on current knowledge of the families. The cropped alignments were formatted to Stockholm format using AlignIO (Biopython; Cock et al., 2009) and then pHMM profiles were created using HMMbuild (HMMER 3.1b2; Eddy, 2011) with the option --singlemx, to enable profile building if only one sequence was given, and default parameters, except MAP (yes) and STATS (LOCAL: MSV / VITERBI / FORWARD). 

The pHMMs were further curated by running HMMsearch (HMMER 3.1b2; Eddy, 2011) on all the proteins which had been used to create the pHMMs. The results of this search were used to guide the selection of the threshold values (Supplementary Figure 18) for grouping sequences into the “classified”, “ambiguously classified” and “unclassified” categories. 

A list of the pHMMs, number of input sequences, cropping coordinates, and the HMMbuild output information is provided in Supplementary Table 9 of the manuscript.

## References
Aiewsakun, P., & Simmonds, P. (2018). ‘The genomic underpinnings of eukaryotic virus taxonomy: creating a sequence-based framework for family-level virus classification’, Microbiome, 6/1: 38. DOI: 10.1186/s40168-018-0422-7

Berman, H. M., Westbrook, J., Feng, Z., Gilliland, G., Bhat, T. N., Weissig, H., Shindyalov, I. N., et al. (2000). ‘The Protein Data Bank’, Nucleic Acids Research, 28/1: 235–42. DOI: 10.1093/nar/28.1.235

Cock, P. J. A., Antao, T., Chang, J. T., Chapman, B. A., Cox, C. J., Dalke, A., Friedberg, I., et al. (2009). ‘Biopython: freely available Python tools for computational molecular biology and bioinformatics’, Bioinformatics, 25/11: 1422–3. DOI: 10.1093/bioinformatics/btp163

Eddy, S. R. (2011). ‘Accelerated Profile HMM Searches’, PLoS computational biology, 7/10: e1002195. DOI: 10.1371/journal.pcbi.1002195

Edgar, R. C. (2004). ‘MUSCLE: multiple sequence alignment with high accuracy and high throughput’, Nucleic Acids Research, 32/5: 1792–7. DOI: 10.1093/nar/gkh340

Finn, R. D., Bateman, A., Clements, J., Coggill, P., Eberhardt, R. Y., Eddy, S. R., Heger, A., et al. (2014). ‘Pfam: the protein families database’, Nucleic Acids Research, 42/Database issue: D222-230. DOI: 10.1093/nar/gkt1223

Zimmermann, L., Stephens, A., Nam, S.-Z., Rau, D., Kübler, J., Lozajic, M., Gabler, F., et al. (2018). ‘A Completely Reimplemented MPI Bioinformatics Toolkit with a New HHpred Server at its Core’, Journal of Molecular Biology, 430/15: 2237–43. DOI: 10.1016/j.jmb.2017.12.007