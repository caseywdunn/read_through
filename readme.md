# Read me for read through


Jupyter notebook with an analysis of codon read through in Drosophila.

## Step 1


Given:
- transcript sequences
- models for the transcripts (orfs, start, stop, etc)

Create a pandas dataframe that has the following:
- Gene id
- AA seqeunce of ORF 1 (canonical orf)
- Stop codon sequence at end of ORF1
- bp following the stop
- length of 3' UTR
- Sequernce of first stop codon after canonical stop, empty string if there is no other stop codon
- translation of ORF2, up to stop codon if present otherwise up to end of stop codon
- Nucleotide sequence of ORF1, starting with start codon
- Nucleotide sequence of ORF2, starting immediately after stop codon


# Step 2

Given a list of which genes have read through externally validated, add a column to dataframe that indicates if gene has read through.

We will use http://www.genome.org/cgi/doi/10.1101/gr.119974.110 . It is based on genome and annotations from flybase.org (Tweedie et al. 2009) release FB2008-10.