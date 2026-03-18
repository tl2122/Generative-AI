---
layout: default
title: "Protein Sequencing Using Masked Language Models with Transformer Architecture"
---
<!-- # Protein Sequencing Using Masked Language Models with Transformer Architecture -->

## Introduction
<p align='center'>
<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/a538cba2-ad37-46ba-944e-de1ba292235e" />
</p>

*Fig 1: Diagram of secondary protein structure showing alpha-helices and beta-sheets, and amino acid chain.*

Proteins are essential ingredients of life, performing a large number of critical functions in the body, including 
catalyzing biochemical reactions and providing structural support. The proteins are made up of amino acids connected 
in a long sequence, which determines its structure and properties. And the structure is key to its function, with the 
arrangement of amino acids  making up its primary structure. The secondary structure involves local folding patterns—such
as alpha-helices, beta-sheets, and coils—that emerge through hydrogen bonding interactions (Fig .1). These patterns are vital
for shaping the protein's overall three-dimensional structure, which ultimately determines its biological role. For example, 
hydrophobicity, polarity, and shape determine protein folding, stability, interactions, and specificity, crucial for enzyme activity
and molecular recognition. X-ray crystallography has long been a powerful method for determining protein structures, offering high-resolution 
images of folded proteins [1]. However, given the inherent complexity of protein sequences and structures, computational approaches,
particularly deep learning, have become indispensable for analyzing and predicting protein structures from sequences.

Deep learning, a subset of machine learning, has shown remarkable success in sequence processing tasks due to its ability to
identify complex patterns within data. Transformers, a specific type of deep learning model, have revolutionized the way sequential
data is handled across many domains. The notable success of AlphaFold algorithm in predicting  protein structure to a very high 
accuracy in CASP13 competition demonstrated the power of AI in solving protein folding challenges, laying the groundwork
for future advancements in protein structure and function analysis [2-5]. 
This achievement underscores the potential of deep learning techniques in addressing complex problems involving 
high-dimensional data, such as protein sequence analysis. The motivation for this study is to explore the application of
masked language modeling using transformer architecture to improve protein sequence analysis and prediction, leveraging 
deep learning to capture complex structural relationships.


## Dataset
The dataset used for this study comes from the UniProt SPROT database,
a well-established resource that contains sequences of proteins from various organisms.
The data consists of amino acid sequences that were tokenized and padded to form dense vectors  
and used for training a transformer model. The computational complexity ($O(L^2)$) of the model
and its performance is proportional to the square of the sequence length. As such, only shorter
sequences with 128 amino acid residues were used. In total, 25,000 protein sequences were included,
with 20,000 sequences designated for training and the remaining 5,000 used for validation. The figures 
below (Fig. 2) illustrate the lengths of the training sequences and the frequency distribution of 
each amino acid residue, showing variations in residue frequencies across the dataset.

<p align =center>
<img width="300" height="305" alt="image" src="https://github.com/user-attachments/assets/dd8c8faf-20c6-4f57-9306-f16ba22c87fa" />
<img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/e574854c-7efe-4399-af37-06a0dbe7fc98" />
</p>

*Fig 2: Length of protein sequences and frequecy of each amino acid residue in the training dataset.*


