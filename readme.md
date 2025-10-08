# Read me for read through

Jupyter notebook with an analysis of codon read through in Drosophila.

## Needed files

These files need to be downloaded and placed in this folder.

Stop codon read through genes. Search for `gene with stop codon read through` for Sequence Ontology at https://flybase.org/vocabularies . Download IDs as `FlyBase_IDs.txt`

Transcript sequences from https://s3ftp.flybase.org/genomes/Drosophila_melanogaster/dmel_r6.64_FB2025_03/fasta/dmel-all-transcript-r6.64.fasta.gz

CDS sequences from https://s3ftp.flybase.org/genomes/Drosophila_melanogaster/dmel_r6.64_FB2025_03/fasta/dmel-all-CDS-r6.64.fasta.gz


## Step 1

Given:
- transcript sequence
- CDS sequences

First ingest the transcripts and CDSs. 

Associate each CDS with its parent transcript, using the parent tag in the CDS header. For example, this CDS:

```
>Nep3-PA type=CDS; loc=X:join(19963955..19964071,19964782..19964944,19965006..19965126,19965197..19965511,19965577..19966071,19966183..19967012,19967081..19967223,19967284..19967460); name=Nep3-RA; dbxref=FlyBase:FBpp0070000,FlyBase_Annotation_IDs:CG9565-PA,REFSEQ:NP_523417,GB_protein:AAF45370,UniProt/Swiss-Prot:Q9W5Y0; MD5=5c3c0b466b23e32d99dfff926a5e8c6b; length=2361; parent=FBgn0031081,FBtr0070000; release=r6.64; species=Dmel; 

```

Goes with this transcript:

```
>FBtr0070000 type=mRNA; loc=X:join(19961689..19961845,19963955..19964071,19964782..19964944,19965006..19965126,19965197..19965511,19965577..19966071,19966183..19967012,19967081..19967223,19967284..19968479); ID=FBtr0070000; name=Nep3-RA; dbxref=FlyBase:FBtr0070000,FlyBase_Annotation_IDs:CG9565-RA,REFSEQ:NM_078693,REFSEQ:NM_078693; MD5=6c3abf7c6ba8b1392a073c85365b2e75; length=3537; parent=FBgn0031081; release=r6.64; species=Dmel; 
```

If there is not a one to one mapping for a CDS or transcript print a warning and skip.

For each gene, align the CDS to the transcript and isolate 5' utr, orf1 (same as CDS), 3' utr. 

Create a data frame with columns:
- gene_id
- 5' utr
- orf1
- 3' utr


## Step 2

Add the following to the data frame:
- AA seqeunce of ORF 1 (canonical orf)
- Stop codon sequence at end of ORF1
- bp following the stop
- length of 3' UTR
- Sequernce of first stop codon after canonical stop, empty string if there is no other stop codon
- translation of ORF2, up to stop codon if present otherwise up to end of stop codon
- Nucleotide sequence of ORF1, starting with start codon
- Nucleotide sequence of ORF2, starting immediately after stop codon


## Step 3

Given the list `Data1_DmelReadthroughCandidates.txt` of which genes have externally validated read through , add a column to dataframe that indicates if gene has read through.

## Other resources

283 readthrough genes from  http://www.genome.org/cgi/doi/10.1101/gr.119974.110, available in their supplemental file `Data1_DmelReadthroughCandidates.txt`. It is based on genome and annotations from flybase.org (Tweedie et al. 2009) release FB2008-10. Those candidates from their sup info have been added to this repo as `Data1_DmelReadthroughCandidates.txt`.
