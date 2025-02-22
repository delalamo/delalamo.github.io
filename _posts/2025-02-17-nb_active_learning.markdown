---
layout: post
title:  "Estimating an antibody's conformational landscape using inverse folding"
date:   2025-02-17 2:19:00
categories: [Science notes]
---
Calculating the full conformational landscape of an antibody, or any medium-sized protein more generally, is computationally expensive. A new preprint introduces a shortcut that could speed this up and accelerate antibody design.

Molecular dynamics simulations and ML-guided inverse folding (structure-based design) naturally complement each other. The former models the conformational landscape of a protein ($$p(struct\|seq)$$), but is expensive as hell, while the latter quickly calculates the likelihood of a sequence given a static structure ($$p(seq\|struct)$$). It's natural to attempt to use the latter as a surrogate function that approximates the former using Bayes's theorem:

$$
p(seq|struct) = \frac{p(struct|seq)p(seq)}{p(struct)}
$$

Plenty of precedent exists for calculating $$p(seq)$$ using methods like protein language models [1,2]. This is not, however, true of $$p(struct)$$: the field has not arrived at a way to calculate the reasonableness of a structure independent of its sequence.

In a recent preprint that combines molecular simulations with inverse folding and active learning, Brotzakis et al sidestep to the need to define $$p(struct)$$ by reframing the problem as a design problem, where the goal is to maximize the reasonableness of a mutant ($$p(seq_{mut})$$) relative to that of the starting sequence ($$p(seq_{wt})$$) [3]. They do this by rearranging the equation as follows:

$$
p(struct|seq_{mut}) = p(struct|seq_{wt}) \frac{p(seq_{mut}|struct)p(seq_{wt})}{p(seq_{wt}|struct)p(seq_{mut})}
$$

The result eliminates the difficult-to-estimate $$p(struct)$$ and allows relative changes in an protein's conformational landscape to be quickly approximated using inverse folding models like ProteinMPNN [4], instead of calculated from scratch using MD, which is far more expensive. (The authors further cut costs by eliminating $$p(seq)$$ from their calculations, stating that the narrow design scope doesn't warrant its inclusion; antibody language models tend to show high uncertainty when calculating likelihoods for those residues anyway [5])

For antibodies in particular, the ability to approximate the accuracy of molecular simulations with cheap machine learning methods could be useful given that ML alone is incapable of accurately modeling the most important substructures of those proteins [6].

The rest of the preprint is short on details, and its main text is only three pages, but I hope the authors further explore this methods development as it could be quite useful.

1. Verkuil et al. ["Language models generalize beyond natural proteins"](doi.org/10.1101/2022.12.21.521521) biorxiv 2022
2. Nijkamp et al. ["Progen2: Exploring the boundaries of protein language models"](doi.org/10.1016/j.cels.2023.10.002) Cell Systems 2023 
3. Brotzakis et al. ["Design of Protein Sequences with Precisely Tuned Kinetic Properties"](doi.org/10.1101/2025.02.13.638027) biorxiv 2025
4. Dauparas et al. ["Robust deep learning-based protein sequence design using ProteinMPNN"](doi.org/10.1126/science.add2187) Science 2022
5. Shuai et al. ["IgLM: Infilling language modeling for antibody sequence design"](doi.org/10.1016/j.cels.2023.10.001) Cell Systems 2023
6. Fernandez-Quintero et al. ["Challenges in antibody structure prediction"](doi.org/10.1080/19420862.2023.2175319) mAbs 2022