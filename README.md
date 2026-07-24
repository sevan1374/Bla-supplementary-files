# Bla-supplementary-files
## Data availability
All metadata and raw data associated with this study are available at the following three links:


Files_1.zip link : https://drive.google.com/file/d/1d-8T2Si4ConVi2eLflQhUAjdWci8QJVt/view?usp=drive_link


Files_2.zip link : https://drive.google.com/file/d/1p_AJOSEFUPecEQ9c3WHST2UDv6LveS1I/view?usp=drive_link


Files_3.zip link : https://drive.google.com/file/d/13U_OPSUuhfCbT8HmCWH-eFfr-IrbysYE/view?usp=drive_link


Zip files Descriptions:

Files_1.zip contains 4 folders, including:

	 1- Beta_lactamases_subgroups: Contains 5 folders with the alignments for all classes of β-lactamases, along with Active_site_motifs.xlsx, which summarizes the active site motifs for each subgroup.

	 2- HMM_files: Includes HMM files for all classes of β-lactamases and RecA (collected from the GTDB HMM database).

	 3- Non_Beta_lactamase_subgroups: Contains 5 folders with alignments for all classes of non-β-lactamases, along with Summary_non-Beta_lactamase.xlsx, which summarizes the structural motifs, active site motifs, and phylogenetic placements of non-β-lactamase subgroups.

	 4- Sequence_files: Includes sequence files for all classes of β-lactamases, as well as RecA.

Files_2.zip contains:
		6 folders, each corresponding to structural data for a specific class or subclass—including metallo-β-lactamases (MBLs)—of non-β-lactamase proteins.
	Within each folder, subdirectories are named according to subgroup identifiers and include both collected and predicted structures.
	An additional msa folder provides the structural alignments for each subgroup, generated using FoldMason.
	The file naming convention follows the format:
	"subgroup_name" + "_" + "class_" + "beta_lactamase_class"
	Each HTML file includes both the structural and sequence alignments for the corresponding subgroup.

Files_3.zip contains:
		6 folders, each corresponding to structural data for a specific class or subclass—including metallo-β-lactamases (MBLs)—of β-lactamase proteins.
	Similar to Files_2.zip, each folder contains subdirectories named by subgroup identifiers, with both collected and predicted structures.
	An msa folder provides the FoldMason-generated structural alignments.
	File names follow the same format:
	"subgroup_name" + "_" + "class_" + "beta_lactamase_class"
	Each HTML file includes both structural and sequence alignments for the respective subgroup.




# β-Lactamase Meta-SSN Sequence Mapper

This tool screens protein sequences against the β-lactamase meta-sequence similarity network (meta-SSN) developed in this study. It combines HMMER screening with BLASTP remapping against curated reference sequences to assign candidate proteins to β-lactamase classes and meta-SSN subgroups.

## Requirements

* Python 3
* Biopython
* HMMER
* BLAST+

The required dependencies can be installed using:

```bash
conda create -n bla-ssn -c conda-forge -c bioconda \
    python=3.11 biopython hmmer blast
conda activate bla-ssn
```

## Usage

Run all available β-lactamase classes:

```bash
python screen_betalactamases.py \
    --input user_sequences.faa \
    --db blactamase_ssn_db \
    --out mapping_results \
    --threads 8
```

Run selected classes only:

```bash
python screen_betalactamases.py \
    --input user_sequences.faa \
    --db blactamase_ssn_db \
    --out mapping_results \
    --threads 8 \
    --families A B1 B3 C D
```

`--input` may be a single protein FASTA file or a directory containing FASTA files.

## Main outputs

* `true_positive_mapping.tsv`: accepted sequences and their predicted classes and meta-SSN subgroups
* `true_positive_sequences.faa`: FASTA file containing accepted sequences
* `false_positive_or_unmapped.tsv`: HMM candidates that could not be mapped above the class-specific threshold
* `ambiguous_multi_class_true_positives.tsv`: sequences assigned to more than one β-lactamase class

Assignments represent sequence-based predictions according to the thresholds and reference dataset used in this study and do not by themselves demonstrate β-lactamase activity.
