This repository contains the RNA virus RNA dependent RNA polymerase (RdRp) pHMMs described in the bioRxiv manuscript available at DOI xxxxx. Methodology is described in full in this manuscript.

# Background Information
Profile Hidden Markov Models (pHMMs) provide a more sensitive method than BLASTP for finding distant homologues of known protein sequences while (in contrast to structure-based approaches) maintaining computational speed (Eddy, 2011). In this analysis, we used known RNA virus sequences to develop 77 family-level RdRp pHMMs. 


# Directory Structure
## alignments
Aligned, Stockholm format files of amino acid sequences used to create the pHMMs.

## pHMMs
Profile HMMs created with HMMER (Eddy, 2011) to represent the alignments.

# Materials and Methods
## Construction of RNA dependent RNA polymerase pHMMs
Initially we used RNA virus groups and sequences from the “GRAViTy” analysis of Aiewsakun and Simmonds (2018). In cases where there was only a small number of sequences in a family-like group, or where some more recently published groups of viruses were not mentioned in Aiewsakun and Simmonds, we searched the NCBI taxonomy and nucleotide databases (April 2018) for additional reference sequences in order to make more representative pHMMs. In total, we used 1,793 RdRp protein and RdRp-containing polyprotein sequences to create 77 pHMMs.

Because many RdRps are contained within longer polyproteins, we wished to trim sequences to a core RdRp region. Therefore, we aligned the sequences within each group with MUSCLE v3.8.31 (Edgar, 2004) and compared the alignments using HHpred (Zimmermann et al., 2018) with the Pfam and PDB databases (Berman et al., 2000; Finn et al., 2014). Based on the second best matching RdRp (to avoid overfitting if the best match Pfam pHMM contained sequences from the same group), we cropped each alignment from both ends. Where appropriate, the alignments and coordinates for trimming were manually curated based on current knowledge of the families. The cropped alignments were formatted to Stockholm format using AlignIO (Biopython; Cock et al., 2009) and then pHMM profiles were created using HMMbuild (HMMER 3.1b2; Eddy, 2011) with the option --singlemx, to enable profile building if only one sequence was given, and default parameters, except MAP (yes) and STATS (LOCAL: MSV / VITERBI / FORWARD). 

The pHMMs were further curated by running HMMsearch (HMMER 3.1b2; Eddy, 2011) on all the proteins which had been used to create the pHMMs. The results of this search were used to guide the selection of the threshold values (Supplementary Figure 18) for grouping sequences into the “classified”, “ambiguously classified” and “unclassified” categories. 

A list of the pHMMs, number of input sequences, cropping coordinates, and the HMMbuild output information is provided in Supplementary Table 9 of the manuscript [link]. 

