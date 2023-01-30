# TRS-omix: search engine.

This code accompanies the paper:
Sebastian Sakowski, Marta Majchrzak, Jacek Waldmajer, Pawel Parniewski: TRS-omix: a new search engine for trinucleotide flanked sequences. 2021.

# Basic terminology

•	TRS means a sequence of three nucleotides, e.g. CCG.

•	TRS motif means a sequence of nucleotides, in which there occurs triple repetition (directly one after another) of the same TRS, e.g. CCGCCGCCG.

•	Class of TRS motifs means TRS motif occurring in one line in the file trs.txt, each of which is preceded by the sign „#”, e.g.: #CCGCCGCCG#CGCCGCCGC#GCCGCCGCC.

•	Number of class of TRS motifs means a natural number (greater than 0), which corresponds to the number of line in the file trs.txt.

•	Flanking sequence means a sequence of nucleotides, in which there occurs at least triple repetition (directly one after another) of the same TRS. 
