# Binder for BVCN Functional Annotation lesson

Initially forked from [here](https://github.com/binder-examples/conda). Thank you to the awesome [binder](https://mybinder.org/) team!

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/Arkadiy-Garber/bvcn-binder-hmmgenie/master?urlpath=lab)

Part of the [Bioinformatics Virtual Coordination Network](https://biovcnet.github.io/) :)

## Walkthrough

Run phmmer on the Cyc1 fasta file

    phmmer -A Cyc1.refseq.msa --tblout Cyc1.refseq.tblout -E 1E-20 Cyc1.faa ../refseq_db/refseq_nr.sample.faa

Build HMM file from MSA (multiple sequence alignment) file, using hmmbuild

    hmmbuild Cyc1.hmm Cyc1.refseq.msa

Query the Cyc1 HMM file against refseq database sample

    hmmsearch --tblout Cyc1.hmm.refseq.tblout Cyc1.hmm ../refseq_db/refseq_nr.sample.faa

Examine the output file. What do the bit scores look like for likely false positives

    less Cyc1.hmm.refseq.tblout

Move into directory containing MtrA FASTA file, and create an alignment using Muscle.

    muscle -in MtrA.faa -out MtrA.fa

Build HMM file from MSA (multiple sequence alignment) file, using hmmbuild

    hmmbuild MtrA.hmm MtrA.fa

Query the MtrA HMM file against refseq database sample

    hmmsearch --tblout MtrA.hmm.nr.tblout MtrA.hmm ../refseq_db/refseq_nr.sample.faa

Examine the output file. What do the bit scores look like for likely false positives

    less MtrA.hmm.nr.tblout

Move the HMM files into a single directory

    mv MtrA.hmm ../HMMs/
    mv Cyc1.hmm ../HMMs/

Check out the Pfam-derived HMM and bitscores.txt file

    less Catalase.hmm

Run HmmGenie (MagicLamp) on test dataset using the new HMM collection

    MagicLamp.py HmmGenie -hmm_dir HMMs/ -hmm_ext hmm -bin_dir test_data/ -bin_ext txt -out hmmgenie_out -eval 1E-1
    MagicLamp.py HmmGenie -hmm_dir HMMs/ -hmm_ext hmm -bin_dir test_data/ -bin_ext txt -out hmmgenie_out -bit HMMs/bitscores.txt
    MagicLamp.py HmmGenie -hmm_dir HMMs/ -hmm_ext hmm -bin_dir test_data/ -bin_ext txt -out hmmgenie_out -bit HMMs/bitscores.txt -clu 2




