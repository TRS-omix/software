# Content of the project: TRS-omix: search engine.
* General info
* Basic terminology
* Description of TRS-omix implementation
* Using TRS-omix

## General info
This repository contains code and TRS-omix software to search trinucleotide repeat sequences (`TRS`) in files of `FASTA type`. This code accompanies the paper: Marta Majchrzak, Sebastian Sakowski, Jacek Waldmajer, and Pawel Parniewski: *New genetic markers differentiating IPEC and ExPEC patotypes. A new approach to genome-wide analysis using a new bioinformatics tool*. 2023.

## Basic terminology

* `TRS` means a sequence of three nucleotides, e.g. CCG.
* `TRS motif` means a nucleotide sequence in which three TRS sequences of the same type are repeated in tandem, e.g. CCGCCGCCG.
* `Class of TRS motifs` means TRS motif occurring in one line in the file `trs.txt`, each of which is preceded by the sign „#”, e.g.: #CCGCCGCCG#CGCCGCCGC#GCCGCCGCC.
* `Number of class of TRS motifs` means a natural number (greater than 0), which corresponds to the number of line in the file `trs.txt`.
* `Flanking sequence` means a sequence of nucleotides, in which there occurs at least triple repetition (repeated in tandem) of the same TRS.
* `Extracted sequence` means a sequence of nucleotides (`SEQ`) which is found between two flanking sequences, that consists of at least one nucleotide and is not a flanking sequence, e.g. TGCTGGC…CATTTCT.
* `Left flanking sequence` (`LSF`) means a flanking sequence which is found seen from the site 5’ of an extracted sequence, e.g.  CCGCCGCCG.
* `Right flanking sequence` (`RSF`) means a flanking sequence which is found seen from the site 3’ of an extracted sequence, e.g. GTGGTGGTG.

## Description of TRS-omix implementation
The TRS-omix search engine was implemented with the use of a GNU compiler collection called `gcc`, compliant with the ISO 2019 of `language C` in the programmers’ environment, bearing the name Code::Blocks (release 20.03) under license from GNU. Below there are the names of constructed data structures given together with their brief description:
* `NPt` – data structure serving to store the position of single nucleotide in the genome and the sign representing this nucleotide.
* `NLt` – data structure serving to store the data on the genome with the use of data structure `NPt`.
* `MPt` – data structure serving to store the number of the TRS motifs, the number of the class of TRS motifs and a single sign representing the nucleotide of the TRS motif from the file `trs.txt`.
* `MLt` – data structure serving to store the TRS motifs contained in the file `trs.txt` with the use of data structure `MPt`.
* `VPt` – data structure serving to store the left and the right positions of the flanking sequence which are found, as well as TRS constituting the base for the flanking sequence. 
* `VLt` – data structure serving to store the position of the flanking sequence.

The individual functional parts of the software were divided into sub-programs (functions). Below all the names of the function are presented, along with a brief functional description.

Main functions:
* `ImportGenome()` – this function imports the genome from the file sequence.fasta and records it in the linked list of `NLt` type.
* `ImportTRSToMLt()` – this function imports TRS motifs from the file `trs.txt` and records them in the linked list of `MLt` type.
* `LC_TRSPositionsFindAndSaveToVLt()` – this function finds the positions of flanking sequences and records them in the linked list `VLt` together with their TRSs which make the base of these flanking sequences for the linear case.
* `LC_InteriorsFindAndSaveToFile()` – this function generates the file `interiors.txt` for the linear case with conditions.
* `CC_TRSPositionsFindAndSaveToVLt()` – this function finds the positions of flanking sequences and records them in the linked list `VLt` together with their TRSs which make the base for these flanking sequences for the linear circular case.
* `CC_InteriorsFindAndSaveToFile()` – this function generates the file `interiors.txt` for the circular case with conditions.

Auxiliary functions:
* `InitNLt()` – this function initializes the linked list of `NLt` type.
* `InitMLt()` – this function initializes the linked list of `MLt` type.
* `InitVLt()` – this function initializes the linked list of `VLt` type.
* `FreeNLt()` – this function frees memory assigned to the linked list of `NLt` type.
* `void FreeMLt()` – this function frees the memory assigned to the linked list of `MLt` type.
* `void FreeVLt()` – this function frees the memory assigned to the linked list of `VLt` type.
* `AddPtToNLt()` – this function adds data of `NPt` type to the linked list of `NLt` type.
* `AddPtToMLt()` – this function adds data of `MPt` type to the linked list of `MLt` type.
* `AddPtToVLt()` – this function adds data of `VPt` type to the linked list of `VLt` type.
* `PrtNLtToFile()` – this function records the content of the linked list in a file.
* `CopyNLt()` – this function creates a copy of the linked list of `NLt` type. 
* `JoinNLtWithNLt()` – this function combines two linked lists of NLt type in such a way that the end of one linked list is added another linked list.
* `FirstToLastInListNLt()` – this function shifts the first element of the linked list `NLt` to the end of the linked list and varies the position and sign representing the nucleotide.

Additional functions:
* `CompareOneTRS()` – this function checks if there occurs one TRS motif.
* `CompareLists()` – this function checks if the TRS repeats itself.
* `FindFistrTRSPosition()` – this function searches the left TRS flanking sequence. 
* `PrintError()` – this function returns information on the basic errors served.
* `UpLe()` – this function replace a small letter representing nucleotide into a capital letter representing nucleotide.
* `ExitN()`, `ExitNN()`, `ExitNM()`, `ExitNMV()` – these functions free the memory assigned to the linked lists of `NLt`, `MLt` and `VLt` types after the occurrence of one of the basic errors served.

Errors Description:
Error Code|Error Description
-------------- | ------
-100|The file `sequence.fasta` is missing, or there is an error with opening `sequence.fasta`.
-110|The data (character) reading error from file `sequence.fasta`.
-120|The data saving error to the linked list NLt.
-130|The file `sequence.fasta` is nucleotides missing.
-140|Initialization error of an additional linked list `NLt`.
-150|The computer memory (RAM) is full or an error while writing a genome nucleotide into memory.
-160|The file `trs.txt` is missing, or there is an error with opening `trs.txt`.
-170|The file `trs.txt` is not formatted correctly. Check record in the `trs.txt` file.
-180|The computer memory (RAM) is full or incorrect record in the trs.txt file.
-190|Check the record of TRS motif in the in the `trs.txt` file.
-200|Incorrect read data (character) from the `trs.txt` file.
-210|The computer memory (RAM) is full or incorrect record of the TRS motif position in the RAM.
-220|The data saving error to the linked list NLt during searching for a TRS motif.
-230|The genome taken from the `sequence.fasta` file contains less nucleotides than the TRS motif.
-240|The computer memory (RAM) is full or an error during writing the flanking sequence of the linear case.
-250|The computer memory (RAM) is full or an error during writing of the TRS motif position in the RAM of the circular case.
-260|The data saving error to the linked list `NLt` or during searching for a TRS motif of the circular case.
-270|The genome taken from the `sequence.fasta` file contains less nucleotides than the TRS motif of the circular case.
-280|The computer memory (RAM) is full or an error during writing the flanking sequence of the circular case.
-290|The file `interiors.txt` creating error of the linear case.
-300|The file `interiors.txt` saving error of the linear case.
-310|The file `interiors.txt` creating error of the circular case.
-320|The file `interiors.txt` saving error of the circular case.

## Using TRS-omix
The TRS-omix software works with the use of files formed in the `FASTA format`. The file called `TRS-omix.exe` is a workable one of TRS-omix search engine.

### Input files. The input files include:
1. `sequence.fasta`,
2. `trs.txt`.

The file called sequence.fasta contains a genome of the examined organism, with the use of which the `TRS-omix` search engine searches for the trinucleotide repeats, and also extracts sequences between such trinucleotide repeats and executes initial analyses of the genome. 
The file `trs.txt` contains classified TRS motifs – each line includes TRS motifs preceded by the sign “#”. One such line is identified as one considered class of TRS motifs. In a similar sense, the file called `trs.txt` is treated as a file with a set of search rules in files of the FASTA type.

### Output file: The output file include:
1. `interiors.txt`.

The file `interiors.txt` contains information on the positions of flanking sequences and also about those and the very extracted sequences themselves. The first line of the file includes headings of 14 columns, while the following lines contain relevant data. The line including the headlines of the columns was formatted in the following way:

`L-NoClass;L-No;LFS;Len(LFS);L-POS(LFS);R-POS(LFS);R-NoClass;R-No;RFS;Len(RFS); L-POS(RFS);R-POS(RFS);>SEQ;Len(SEQ)`

where:
* `L-NoClass` – denotes the number of the class of TRS motifs from the file trs.txt for the left flanking sequence;
* `L-No` – denotes the number of TRS motifs from the file trs.txt for the left flanking sequence;
* `LFS` – denotes the left flanking sequence;
* `Len(LFS)` – denotes the number of nucleotides of the left flanking sequence;
* `L-POS(LFS)` – denotes the position from which the left flanking sequence begins in the genome;
* `R-POS(LFS)` – denotes the position at which the left flanking sequence ends in the genome;
* `R-NoClass` – denotes the number of the class of TRS motifs from the file trs.txt for the right flanking sequence;
* `R-No` – denotes the number of the TRS motif from the file trs.txt for the right flanking sequence;
* `RSF` – denotes the right flanking sequence;
* `Len(RFS)` – denotes the number of nucleotides of the right flanking sequence;
* `L-POS(RFS)` – denotes the position from which right flanking sequence starts in the genome;
* `R-POS(RFS)` – denotes the position at which the right flanking sequence ends in the genome;
* `>` – denotes the place from which the extracted sequence begins; 
*	`SEQ` – denotes the extracted sequence;
*	`Len(SEQ)` – denotes the number of nucleotides of the extracted sequence;

### TRS-omix software options: On starting the executable file of TRS-omix, there appear on the computer screen two options which are possible to select:

1. Analysis of the linear case with conditions: use of this option enables to search TRS motifs in linear genomes with additional search conditions: giving the minimal (`Min`) and maximal (`Max`) length of the searched sequence found between the flanking sequence.
2. Analysis of the circular case with conditions: use of this option enables to search TRS motifs in circle genomes with analogous additional search conditions like in the case of Analysis of the linear case with conditions.
