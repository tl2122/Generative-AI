---
layout: default
title: "Protein Sequencing Using Masked Language Models with Transformer Architecture"
---
# Protein Sequencing Using Masked Language Models with Transformer Architecture

## Abstract
Proteins, fundamental to life’s myriad functions, are encoded by intricate sequences 
of amino acids, where their structure directly dictates their biological role. Understanding 
this structure is crucial for advancing fields like drug design and molecular biology.  
This study investigates the application of masked language modeling—an innovative deep learning approach—using a BERT-style 
transformer architecture  for protein sequence prediction. The model was successfull in learning structural 
properties and relationships between amino acids, demonstrating effectiveness of this approach, 
while its performance was limited by the size of the dataset and computation. This work lays
the foundation for using AI to decode the complexity of proteins, offering exciting possibilities 
for the future of biological research and medical advancements.

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
and used for training a transformer model. The computational complexity ($`O(L^2)`$) of the model
and its performance is proportional to the square of the sequence length. As such, only shorter
sequences with 128 amino acid residues were used. In total, 25,000 protein sequences were included,
with 20,000 sequences designated for training and the remaining 5,000 used for validation. The figures 
below (Fig. 2) illustrate the lengths of the training sequences and the frequency distribution of 
each amino acid residue, showing variations in residue frequencies across the dataset.

<p align =center>
<img width="300" height="305" alt="image" src="https://github.com/user-attachments/assets/dd8c8faf-20c6-4f57-9306-f16ba22c87fa" />
<img width="300" height="300" alt="image" src="https://github.com/user-attachments/assets/e574854c-7efe-4399-af37-06a0dbe7fc98" />
</p>
*Fig 2: Length of protein sequences and frequecy of each amino acid residue (20 canonical + 3 ambiguous- B,X,Z) 
in the training dataset.*


## Modeling Protein Sequences
In recent years, techniques from natural language processing (NLP), particularly masked language modeling, 
have been adopted for biological sequence analysis. The idea behind masked language modeling is to mask 
a certain percentage of the input sequence and train the model to predict the missing tokens based on the context 
of the remaining sequence [6]. This concept has been extended to protein sequences, where amino acid residues are 
masked and the model is tasked with predicting these residues from the surrounding context. In this study, a BERT-style 
transformer model was employed for protein sequence analysis, with a maximum of 20% of the amino acid residues randomly masked during training.
A major advantage of transformers, such as BERT, is that they read the entire sequence at once and process
it bidirectionally, meaning that the model can capture long-range dependencies between amino acid residues. 
This is crucial for understanding protein structures, as the function and shape of a protein are determined not only by 
the immediate interactions between adjacent residues but also by more distant interactions that can influence the protein’s 
overall conformation. In this context, the transformer model was expected to capture structural properties such as hydrophobicity, 
shape, and long-range dependencies in protein sequences.


## Transformer Model
<p>
The BERT-style transformer architecture is used for protein sequence prediction incorporates 
self-attention mechanisms, positional encoding, feedforward networks, and layer normalization. 
Unlike other transformers, which often rely on autoregressive, unidirectional generation, BERT uses a 
bidirectional encoder with masked language modeling for more comprehensive context understanding.

The model incorporates 20 canonical amino acids and 3 ambiguous/unknown amino acids (B, X, Z),
resulting in a total of 23 "amino acid" tokens. The hyperparameters, such as the number of attention heads 
and layers, were selected to provide best model accuracy possible  given the dataset and model size. 
A sequence length of 130 residues was chosen as the maximum input length to ensure efficient training. 
The training loss and accuracy, as well trained confusion matrix from the validation data is shown below. 
<img width="200" height="450" alt="image" src="https://github.com/user-attachments/assets/ec8f5cd4-b6ae-40c5-a67a-0d41a3b7b38b" align="right"/>
*Transformer Model*
</p>

For this study, the following model parameters were used:
```
model = ProteinTransformer(
    vocab_size=26,
    d_model=256,
    num_heads=8,
    num_layers=4,
    d_ff=1024,
    max_len=130,
    pad_token_id=token2idx["[PAD]"]
)
```


| Layer	         |Individual Layer Parameters         |	Total Parameters  |
|:--------------:|:----------------------------------:|:-----------------:|
|Token Emb       |  Embedding (26, 256)               |	6,656             |
|Position Emb	   |  Embedding (130, 256)              | 33,280            |
|Transformer (x4)|	Attention, Feedforward, LayerNorm	| 4,724,736         |
| Total          |	                                  |	4,771,850         |



## Training the Model
The model was trained on the 20,000 protein sequences with a maximum sequence length of 128 residues,
while 5,000 sequences were reserved for validation. Training was conducted with the goal of balancing 
the complexity of the model with the available data and computational resources.
The model achieved approximately 40% accuracy on the training set and 35% accuracy on the validation set. 
These results highlight the model's ability to learn the underlying relationships in the sequences,
although further improvements would require larger models and access to more extensive computation 
capable of handling longer sequences. For a model with 4M parameters and 20k dataset, the accuracy is reasonable [7], 
while the baseline accuracy from random guess is 1/23 ~ 4.5%. 
<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/41680af4-b068-4b5c-a7e9-048572d2824b" />
<img width="400" height="320" alt="image" src="https://github.com/user-attachments/assets/f85529a8-f4b7-4ee8-940e-7793c513cf0e" />
*Loss and Accuracy, confusion Matrix*


## Analysis using Embeddings
Embeddings refer to the process of representing high-dimensional input data in a lower-dimensional space. 
In the context of the transformer model, embeddings are learned representations of the input sequences 
that capture semantic and structural information about the sequences. Using t-SNE (t-distributed Stochastic Neighbor Embedding),
the high-dimensional embeddings were projected in a 2D space. The resulting plot revealed a large central cluster, representing 
sequences that are highly similar to each other, with multiple smaller clusters in the periphery. These smaller clusters likely 
correspond to sequences that belong to distinct protein families or exhibit unique secondary structures. The visualization 
suggests that the model has learned to encode meaningful relationships between protein sequences, such as  evolutionary or functional similarity.
Furthermore, k-Means clustering was applied to group the embeddings into 20 distinct clusters. The resulting 2D 
clusters from the k-Means algorithm provide insight into how protein sequences with similar structural properties 
(e.g. hydrophobicity, secondary structure) group together in the embedding space. Altough the exact properties 
represented here would require further analysis, these findings are important for understanding how the transformer model 
captures protein sequence relationships and structural features.
<img width="700" height="350" alt="image" src="https://github.com/user-attachments/assets/6372bd6b-f003-48ff-a05b-a6d1bcb9a14d" />

*2d Embeddings*


<img width="450" height="400" alt="image" src="https://github.com/user-attachments/assets/aa5b28b2-def0-4afa-8c6c-4f2aa86875c3" />
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/b8f65b56-a573-4fec-a89b-c1166fc9ea22" />

*Embeddings vs Seq length, k-means clusters*




## Conclusion
In this study, a transformer model based on the BERT architecture was successfully applied to protein sequence prediction. 
Trained on 25,000 protein sequences, the model demonstrated effectiveness of using masked language modeling for 
protein sequence analysis. While the model's performance is driven by dataset size and model size, the results show that 
transformers can successfully capture relationships in protein sequences. Future work will focus on scaling the dataset,
enhancing the model’s complexity, and leveraging greater resources to achieve higher accuracy and deeper insights into 
protein structure and function.

<!--
## References
1. Rupp, B. (2010). *Biomolecular Crystallography: Principles, Practice, and Application. Garland Science*.
2. L. AlQuraishi, *AlphaFold: Using AI for scientific discovery* Nature, vol. 591, pp. 222-224, 2020.
3. Vaswani et al., *Attention is all you need* NeurIPS, 2017.
4. M. K. Jones, et al., *Using deep learning models for protein sequence prediction* Bioinformatics, vol. 35, pp. 4621-4630, 2019.
5. J. Jumper, et al., *Highly accurate protein structure prediction with AlphaFold* Nature, vol. 596, pp. 583-589, 2020.
6. IBM, *Masked language models: Unlocking new possibilities with deep learning*,  ibm.com/think/topics/masked-language-model
7. Brandes, N., Ofer, D., Peleg, Y., Rappoport, N., & Linial, M. *ProteinBERT: A universal deep-learning model of protein sequence and function. Bioinformatics*, 38(8), 2102–2110. doi.org/10.1093/bioinformatics/btac020
-->
