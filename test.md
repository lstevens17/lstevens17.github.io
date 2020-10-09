---
permalink: /test/
---

# Scripts and files associated with the _C. bovis_ manuscript

---

### Recipricol best BLAST hits 
To define single-copy orthologues between _C. bovis_ and _C. elegans_, we used a recipricol best BLAST hit approach. We first filtered the protein 
FASTAs so that only the longest isoform of each gene was present. We then used BLASTP to search each proteome against the other like so:

```
blastp -query CBOVIS.caenorhabditis_bovis.v1.proteins.faa_longest_isoforms -db CBOVIS.caenorhabditis_bovis.v1.proteins.faa_longest_isoforms -outfmt 
'6 qseqid sseqid pident mismatch gapopen qstart qend sstart send evalue bitscore qcovs qcovhsp qlen slen length' -num_threads 16 
>CBOVIS_vs_CELEG.blastp.txt
blastp -query CELEG.caenorhabditis_elegans_N2_PRJNA13758_WBPS12.proteins.faa_longest_isoforms -db 
CELEG.caenorhabditis_elegans_N2_PRJNA13758_WBPS12.proteins.faa_longest_isoforms -outfmt '6 qseqid sseqid pident mismatch gapopen qstart qend sstart 
send evalue bitscore qcovs qcovhsp qlen slen length' -num_threads 16 >CELEG_vs_CBOVIS.blastp.txt
```

We then provided these output files to a script written by Dom Laetsch (and available here 
https://github.com/DRL/GenomeBiology2016_globodera_rostochiensis) to define orthogues like so: 

```
./rbbh.py CBOVIS_vs_CELEG.blastp.txt CBOVIS.caenorhabditis_bovis.v1.proteins.faa_longest_isoforms CELEG_vs_CBOVIS.blastp.txt 
CELEG.caenorhabditis_elegans_N2_PRJNA13758_WBPS12.proteins.faa_longest_isoforms 1e-25 75 >CBOVIS_CELEG.rbbh.txt
```
