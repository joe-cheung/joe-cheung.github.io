---
title:  "Did DeepMind Solve The Protein Folding Problem?"
subtitle:
date:   2020-12-15 00:00:00
update:
author: Joe Cheung
description:
tags: science AI
---
*[Epistemic status: I have no expertise, but below is my best guess from what I have read so far, mostly relying on AlQuraishi's excellent [<span class="underline">essay</span>](https://moalquraishi.wordpress.com/2020/12/08/alphafold2-casp14-it-feels-like-ones-child-has-left-home/). The first half of this post will be kind of a literature review on the protein structure prediction, and the second half is a bit of a rehash of AlQuraishi’s essay, so post will serve as a companion piece of sorts to help you understand the background of the problem better if you’re a layman like me.]*

1. TOC
{:toc}

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image2.png)
*[<span class="underline">Obligatory XKCD</span>](https://xkcd.com/1430/)*

DeepMind, Google’s premier AI offshoot, predicted protein structures so impressively with their AlphaFold 2 (AF2) in the Critical Assessment of Techniques for Protein Structure Prediction (CASP), the biennial international competition of at predicting protein structure, that the organisers [<span class="underline">declare</span>](https://predictioncenter.org/casp14/doc/CASP14_press_release.html) the protein structure prediction problem for single protein chains to be solved.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image37.gif)
*[<span class="underline">They see me foldin’ they hatin'</span>](https://deepmind.com/blog/article/AlphaFold-Using-AI-for-scientific-discovery)*

Is the hype for real?[^7] Mohammed AlQuraishi, a computational biologist at Columbia University and CASP participant, said,

  > “In my read of most CASP14 attendees (virtual as it was), I sense that \[the protein structure prediction problem for single protein chains was solved\] was the conclusion of the majority. It certainly is my conclusion as well.”

As if it wasn’t hyperbolic to describe this moment to be protein structure prediction’s [<span class="underline">ImageNet</span>](https://www.wikiwand.com/en/ImageNet) moment like some have, AlQuraishi said,

  > “It is more akin to having the ImageNet accuracies of 2020 in 2012\! A seismic and unprecedented shift so profound it literally turns a field upside down over night.”

## But Why?

The [<span class="underline">central dogma of molecular biology</span>](https://www.wikiwand.com/en/Central_dogma_of_molecular_biology) states that the flow of genetic information within a biological system cannot be transferred back from protein to either protein or nucleic acid per [<span class="underline">Francis Crick</span>](https://www.wikiwand.com/en/Francis_Crick)’s [<span class="underline">original</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5602739/#pbio.2003243.ref001) [<span class="underline">statement</span>](http://libgallery.cshl.edu/items/show/52220) in 1957 . The more popular version as [<span class="underline">stated</span>](https://faseb.onlinelibrary.wiley.com/doi/10.1096/fj.15-1101ufm) by [<span class="underline">James Watson</span>](https://www.wikiwand.com/en/James_Watson) in 1965 is often known as "DNA makes RNA, and RNA makes protein (amino acid sequence)"

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image14.png)
*[<span class="underline">After sequencing a protein’s DNA, we can just look up which letters in the sequence correspond to which amino acid.</span>](https://www.jargonwall.com/molecular-biology/translation/)*

However, we still can’t tell what the function of the protein is until we learn about its structure because [<span class="underline">structure is function</span>](https://www.ncbi.nlm.nih.gov/books/NBK217812/): how a protein works and what it does is determined by its [native (properly-folded) <span class="underline">conformation</span>](https://www.wikiwand.com/en/Protein_structure) (3D shape).

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image39.png)
*[<span class="underline">1D amino acid sequence fold into 3D blobs</span>](https://deepmind.com/blog/article/AlphaFold-Using-AI-for-scientific-discovery)*

To determine the structure of a protein, the predominant approach is to look at its conformational changes during gradual unfolding or folding with [<span class="underline">experimental techniques</span>](https://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/methods-for-determining-structure#:~:text=Several%20methods%20are%20currently%20used,method%20has%20advantages%20and%20disadvantages.) (e.g. [<span class="underline">X-ray crystallography</span>](https://www.wikiwand.com/en/X-ray_crystallography#:~:text=X%2Dray%20crystallography%20\(XRC\),diffract%20into%20many%20specific%20directions.), [<span class="underline">nuclear magnetic resonance spectroscopy</span>](https://www.wikiwand.com/en/Nuclear_magnetic_resonance_spectroscopy_of_proteins), and more recently [<span class="underline">cryogenic electron microscopy</span>](https://www.wikiwand.com/en/Cryogenic_electron_microscopy) a.k.a. cryo-EM).

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image31.png)

*[<span class="underline">Steps of X-ray crystallography</span>](https://www.sciencedirect.com/science/article/abs/pii/S1438422114001775)*

As these methods depend on extensive trial and error, it can take years of painstaking and laborious work per structure, and require the use of multi-million dollar specialised equipment. For example, it [<span class="underline">takes</span>](https://towardsdatascience.com/unfolding-alphafold-683d576a54a3) about a year and $120000 to obtain the structure of a single protein with X-ray crystallography. Worse, they don’t work for all proteins. Notably, membrane proteins (e.g. the ACE2 receptor that SARS-CoV-2 binds to) are [<span class="underline">difficult</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3641781/) to crystallise, yet they represent the [<span class="underline">majority</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4379170/) of drug targets.

This means that we have only determined the structure of a tiny percentage of proteins we've sequenced: there are more than 200M protein sequences in the [<span class="underline">Universal Protein Reference Clusters</span>](https://www.uniprot.org/) (UniRef), but only 170k structures in the [<span class="underline">Protein Data Bank</span>](https://www.rcsb.org/) (PDB), and the gap is only widening as genome sequencing has been improving at a breathtaking rate.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image26.png)
*[<span class="underline">Sequencing will continue until morale improves.</span>](https://moalquraishi.wordpress.com/2019/04/01/the-future-of-protein-science-will-not-be-supervised/)*

When [<span class="underline">Christian Anfinsen</span>](https://www.wikiwand.com/en/Anfinsen%27s_dogma) won the 1972 [<span class="underline">Nobel Prize</span>](https://www.nobelprize.org/prizes/chemistry/1972/summary/) in Chemistry for [<span class="underline">Anfinsen's dogma</span>](https://www.wikiwand.com/en/Anfinsen%27s_dogma) (a.k.a. the [<span class="underline">thermodynamic hypothesis</span>](https://science.sciencemag.org/content/181/4096/223)), he [<span class="underline">postulated</span>](https://www.nobelprize.org/uploads/2018/06/anfinsen-lecture.pdf) that to determine a protein's native structure, all the information you need is in its amino-acid sequence. So what if we could determine the 3D structures of proteins much faster and much faster by folding amino acid sequences *in silico*?

In the 6 decades since the [<span class="underline">1962 Nobel Prize in Chemistry</span>](https://www.nobelprize.org/prizes/chemistry/1962/summary/) was awarded to [<span class="underline">Max Perutz</span>](https://www.wikiwand.com/en/Max_Perutz) and [<span class="underline">John Kendrew</span>](https://www.wikiwand.com/en/John_Kendrew) for founding the field of structural biology, the [<span class="underline">protein-folding problem</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2443096/#:~:text=The%20protein%20folding%20problem%20is,first%20atomic%2Dresolution%20protein%20structures.) actually came to be three main questions:

1. *The physical folding code*: How is the 3D native (properly-folded/functional) structure of a protein determined by the physicochemical properties that are encoded in its 1D amino-acid sequence?[^1]

2. *The folding mechanism*: A polypeptide chain has an almost unfathomable number of possible conformations. How can proteins fold so fast?[^2]

3. *Predicting protein structures using computers*: Can we devise a computer algorithm to predict a protein’s native structure from its amino acid sequence?

So whenever you hear people shout that DeepMind has solved the grand challenge of the protein folding problem, they’re really only referring to the [<span class="underline">protein structure prediction problem</span>](https://en.wikipedia.org/wiki/Protein_structure_prediction?oldformat=true).

## A Very Hard Problem

So you want to predict protein structure *in silico*, the obvious way is to simulate physics. With [<span class="underline">molecular dynamics</span>](https://www.nature.com/articles/nsb0902-646) (MD), you can try to model the forces on each atom, given its location, charge, and chemical bonds, then calculate accelerations and velocities and evolve the system step by step. [<span class="underline">However</span>](https://rootsofprogress.org/alphafold-protein-folding-explainer), a typical protein has hundreds of residues (amino acids), which means thousands of atoms. Then there are the like 30k more atoms to simulate because of surrounding water molecules. And there are electrostatic interactions between every pair of atoms. So naively that’s ~450M pairs.

Simulating physics has the [<span class="underline">Big-O</span>](https://www.wikiwand.com/en/Time_complexity) complexity of O(n<sup>2</sup>), shown as the turquoise line in the graph below. (There are smart algorithms to make this O(N log N).) More like Big Oof complexity because you end up needing to run for something like 10<sup>9</sup> to 10<sup>12</sup> time-steps[^5].

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image18.png)

*[<span class="underline">Big-O notation represents the upper bound of the complexity of an algorithm, where n is the input size in bits, assuming each operation takes the same unit time-step to perform.</span>](https://stackoverflow.com/questions/487258/what-is-a-plain-english-explanation-of-big-o-notation)*

Just when you’re questioning your hubris, you remember that Anfinsen’s dogma[^3] also postulates that a protein’s native structure has the minimal global free energy, so maybe you can use the same MD model to calculate what structure minimises free energy the most. You do this by sampling the [<span class="underline">configuration space</span>](https://www.wikiwand.com/en/Configuration_space_\(physics\)) (set of all possible conformations), guided by scoring functions (potential-energy minimising) to produce a large set of candidates, then selecting the better ones with more scoring functions, before high-resolution refining. But as Cyrus Levinthal [<span class="underline">noted</span>](https://web.archive.org/web/20050212130449/http://paradox.harvard.edu/~igor/PUBL_BER/PUB22.pdf) in 1969, the number of possible conformations is astronomically large, like 10<sup>300</sup> (\!) large. It will take you more time than the age of the universe to solve the 2 main problems of calculating the protein free energy and finding the global minimum of that energy. 2D and 3D mathematical modelling of protein folding as a free energy minimisation problem is [<span class="underline">NP-hard</span>](https://www.gwern.net/docs/biology/1993-fraenkel.pdf)\!

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image4.png)
*[<span class="underline">Protein folding time given 2 degrees of freedom and 3 possible positions for each peptide bond, and assuming 1 nanosecond spent to sample each conformation.</span>](https://blog.exxactcorp.com/deepminds-protein-folding-upset/)*

## So You Want To Predict Protein Structures

**<span class="underline">3.1. Conformation initialisation</span>**

Protein structure prediction methods are categorised into [<span class="underline">template-based modelling</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2680823/) (TBM) and [<span class="underline">free modelling</span>](https://www.wikiwand.com/en/De_novo_protein_structure_prediction) (FM) with the key difference in how they arrive at the initial conformation. In fact, both categories of prediction methods make use of the structural information from previously solved structures in the PDB to [<span class="underline">after conformation</span> <span class="underline">initialisation</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6407873/), as the basic observation is that similar sequences from the same evolutionary family often adopt similar protein structures.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image3.png)
*[<span class="underline">Broad classification of a few Computational PSP approaches developed and used to determine protein structure.</span>](https://www.sciencedirect.com/science/article/abs/pii/S0300908420300961?via%3Dihub)*

The computational-intensive problems of calculating the protein free energy and finding the global minimum of that energy can be partially bypassed in TBM, in which the search space is pruned by the assumption that the protein in question adopts a structure that is close to the experimentally determined structure of another homologous protein. The steps in the canonical [<span class="underline">procedure</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4108304/) of the TBM are:

1. finding known structures (templates) in the PDB related to the sequence to be modeled (target);

2. aligning the target sequence to the template structure;

3. building structural frameworks by copying the aligned regions or by satisfying the spatial restraints from templates;

4. constructing the unaligned loop regions and add side-chain atoms;

5. evaluating the model using a variety of internal and external criteria.

On the basis of shared sequence identity, TBM can be classified into:

  - *[<span class="underline">Homology Modelling</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5654859/) (HM)*: for target proteins that have homologous proteins with known structure (usually from the same family/share ancestry), compares 1D target sequence to 1D template sequence;

  - *[<span class="underline">Comparative Modelling</span>](https://www.wikiwand.com/en/Homology_modeling#:~:text=Homology%20modeling%2C%20also%20known%20as,\(the%20%22template%22\).) (CM)*: for target proteins that have no identified evolutionary relationship with the template but only shared sequence similarity, compares 1D target sequence to 1D template sequence

  - and *[<span class="underline">Protein Threading</span>](https://www.wikiwand.com/en/Threading_\(protein_sequence\)) (a.k.a. fold-recognition)*: for target proteins that do not have homologous proteins with known structure, but have the same fold as known structures, compares 1D target sequence and 3D template structure by "threading" (i.e. placing, aligning) each amino acid in the target sequence to a position in the template structure and evaluating how well the target fits the template

HM and CM are effective as long as the target sequence shares at least [<span class="underline">25</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4108304/)-[<span class="underline">30%</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4559291/) identity with the template. For any target lower than that, threading is used.

If you think TBM is too easy, you can try FM (a.k.a. template-free or *ab initio* or *de novo* simulation), where no solved homologue of the protein target is used, so you have to explicitly resolve the computationally-intensive problems. Sometimes you don’t really have a choice because a significant amount of target sequences aren’t homologous with well-studied protein families. [<span class="underline">There are</span>](https://www.sciencedirect.com/science/article/abs/pii/S0300908420300961?via%3Dihub):

  - *Physics-based approaches*: good luck

  - *Fragment-based approaches (FBA):* by far the most successful, first predict the backbone dihedral angle, solvent accessibility, contact map or secondary structure segments of the target sequence, then replace the sequence with fragments cut from known structures in the PDB based on those predictions

  - *Secondary-structure-elements- (SSE) based approaches*: assembling the core backbone of the protein with an exception of loop regions leading to model refinement protocols

Whether you’re doing TBM or FM or a hybrid of both, you will be mixing and matching residues, which makes the side chain conformations from template unusable, so the initial reduced conformation you get only has the backbone carbon atoms (Cα). For example, each residue can be represented just by its Cα-atom and the virtual center of its side chain, or the entire backbone conformation can be represented by a series of dihedral angles, which allows you to cut down a lot of time.

**<span class="underline">3.2: Conformational search and structure selection</span>**

Searching through the conformation space requires a “[<span class="underline">force field</span>](https://en.wikipedia.org/wiki/Force_field_(chemistry)?oldformat=true))” depicting the protein conformational energy landscape, where all conformations correspond to a point on the energy landscape (the native conformation should be the lowest point).

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image22.png)

*[<span class="underline">Protein folding guided by funnel-shaped energy landscape</span>](https://pubmed.ncbi.nlm.nih.gov/23180855/)*

Proteins fold due to atomic interactions, so ideally force fields should be constructed based on quantum mechanics. Alas, until quantum computers materialise, you can only construct force fields based on classical physics that consist of the bond-stretching energy, the angle bending energy, the angle torsional energy and other energies for nonbonded interactions. Due to computational limits, these [<span class="underline">physics-based energy functions</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4554537/) are often inaccurate for describing the complicated atomic interactions and have poor performances in protein structure prediction.

On the other hand, you can use [<span class="underline">force fields</span>](https://www.wikiwand.com/en/Statistical_potential) constructed based on information such as distance, dihedral angles, solvent accessibility, and side chain orientation of the many experimentally-determined structures in the PDB. This is where machine learning methods like [<span class="underline">hidden Markov models</span>](https://www2.cs.duke.edu/courses/cps160/compsci260/fall14/resources/HMM/eddy96.pdf), [<span class="underline">artificial neural networks</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC286422/pdf/pnas00241-0168.pdf), and [<span class="underline">support vector machines</span>](https://academic.oup.com/nar/article/36/9/3025/1104168) come to play. This unfortunately means that such [<span class="underline">knowledge-based energy functions</span>](https://link.springer.com/chapter/10.1007/978-0-387-68372-0_3) are constructed with “[<span class="underline">black boxes</span>](https://towardsdatascience.com/machine-learning-how-black-is-this-black-box-f11e4031fdf)” which cannot help you understand the nature of the protein folding dynamics.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image29.png)
*[<span class="underline">Overview of Alpha Fold the first</span>](https://towardsdatascience.com/unfolding-alphafold-683d576a54a3)*

In [<span class="underline">practice</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4108304/), most structure prediction methods employ both physics-based and knowledge-based energy functions, with which you have to find a proper way to search for the minimal global free energy conformation of the target protein. One way is MD, but if you recall, that’ll take more time than the age of the universe. Worse, to make statistically valid conclusions from the simulations, the time span simulated should match the kinetics of the natural process, otherwise it’s like making conclusions about how a human walks by only looking at less than one footstep. The time step of MD is generally in the order of femtosecond (10<sup>−15</sup> s), while the [<span class="underline">time</span>](https://www.sciencedirect.com/science/article/pii/S1359027897000023?via%3Dihub) required for protein folding is usually in milliseconds (10<sup>−3</sup> s). Yeah that’s right, as if MD doesn’t already take long enough, each time step should be a trillion times slower.

A much faster method for conformation search is based on [<span class="underline">Monte</span>](https://www.wikiwand.com/en/Monte_Carlo_method) [<span class="underline">Carlo</span>](https://www.biorxiv.org/content/10.1101/361527v1.full) [<span class="underline">simulation</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC299132/?page=1), which randomly changes the conformation based on various movements designed beforehand that includes the shifts and rotations of structural segments as well as the position changes of a single atom. These movements can be spatially continuous, or confined to a cubic lattice system, which can dramatically reduce the conformation space.

Whether you’re using MD or Monte Carlo simulations, your force field will not be good enough so the conformations are often trapped at the local minimal state, even when the global minimal state is identified. Hence, the common procedure during simulation is to regularly output lower energy intermediate structures. In fact, there is a specific [<span class="underline">category</span>](https://onlinelibrary.wiley.com/doi/full/10.1002/prot.24347) in CASP for assessing the methods of structural quality assessment to check which of the many conformations you end up with is actually the native one. You can perform structure selection with energy functions much more complicated than the ones you use for conformation search because you have a lot fewer conformations to choose from.

**<span class="underline">3.3: All-atom structure reconstruction and structure refinement</span>**

Now you end up with just one or several reduced structural models with only the Cα-atoms, so you have to rebuild the backbone atoms (carbon, nitrogen, oxygen) and the side chain for every residue using fragments cut from experimental structures.

Unfortunately the all-atom model isn’t very good due to defects of the force field, conformational search or all-atom reconstruction, so you need to slightly tweak the local details of the backbone conformation with more MD or Monte Carlo simulations. In fact, there is also a specific category for model refinement since CASP7.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image8.png)
*[<span class="underline">Refining</span>](https://brettkoonce.com/talks/an-introduction-to-alphafold-and-protein-modeling/)*

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image1.png)

*[<span class="underline">Hopefully this flowchart of TBM and FM now makes sense.</span>](https://brettkoonce.com/talks/an-introduction-to-alphafold-and-protein-modeling/)*

## CASP

To compare the different protein structure prediction approaches, we can look at their performances in the Critical Assessment of Techniques for Protein Structure Prediction (CASP), a double-blinded “world championship” held every 2 years since [<span class="underline">1994</span>](https://onlinelibrary.wiley.com/doi/abs/10.1002/prot.340230303), where ~100 teams try to predict ~100 domains of protein native structures that have been recently solved (overwhelmingly by the US [<span class="underline">Protein Structure Initiative</span>](https://www.wikiwand.com/en/Protein_Structure_Initiative)) and temporarily withheld from PDB.

There are many categories such as multimeric targets (for protein complexes), and refinement targets, but the two categories relevant to AlphaFold are tertiary structure prediction and contact (or distance) prediction.

CASP structures have on average grown in length, although the vast majority of structures remain shorter than 1,000 residues:

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image20.png)
*[<span class="underline">Length distribution of proteins in CASP 7 through 12, broken down by difficulty class. Pie charts show the number of proteins per difficulty class.</span>](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-019-2932-0)*

The average difficulty of the targets in CASP has also increased. In fact, the targets for CASP14 were the most difficult to date:

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image21.png)

*[<span class="underline">Comparison of the targets of the last four CASPs in terms of the coverage and sequence identity of the available templates.</span>](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/?s=09)*

There are 2 types of predictors: the human, and the server. For each protein target, the former has 3 weeks and can make use of all the server results and any available resources, while the latter only has 3 days and cannot see the result from other servers. As it is “openbook” for humans, they can easily beat most of the servers by simply doing a consensus analysis (majority voting) on all server predictions, or straight up just copying the results from the best servers.

One metric used by CASP is the [<span class="underline">global distance test</span>](https://www.wikiwand.com/en/Global_distance_test) “total score” (GDT\_TS) from 0-100 (the higher the better). It is calculated by superimposing the predicted tertiary structure onto the experimentally determined (via [<span class="underline">X-ray crystallography</span>](https://www.wikiwand.com/en/X-ray_crystallography) or [<span class="underline">protein NMR</span>](https://www.wikiwand.com/en/Nuclear_magnetic_resonance_spectroscopy_of_proteins)) tertiary structure, and adding the percentage of alpha carbons (first carbon atom that attaches to a functional group) that fall within cutoffs of 1, 2, 4, and 8 Å (10<sup>−10</sup> m), then divide the sum by 4.

What’s a [<span class="underline">good score</span>](https://moalquraishi.wordpress.com/2020/12/08/alphafold2-casp14-it-feels-like-ones-child-has-left-home/)? Random predictions give around 20 GDT; getting the gross topology right gets one to about 50-60 GDT; accurate topology is usually around 70-80 GDT; and when even the side-chain conformations are correct, GDT\_TS begins to climb above 90 GDT; and anything above 95 GDT is within experimental accuracy. According to [<span class="underline">John Moult</span>](http://moult.ibbr.umd.edu/), one of the founders of CASP who [<span class="underline">declared</span>](https://predictioncenter.org/casp14/doc/CASP14_press_release.html) AF2 has solved protein structure prediction for single protein chains, around 90 GDT is informally considered to be competitive with results obtained from experimental methods.

Another metric that is more commonly used by the broader biology community is the [<span class="underline">root-mean-square deviation</span>](https://www.wikiwand.com/en/Root-mean-square_deviation_of_atomic_positions) (RMSD). It is calculated by taking the root mean square of the distance between alpha carbons of the superimposed structures. RMSD is sometimes expressed as RMS\_CA or Cα-RMSD, as it only looks at alpha carbons, while RMS\_ALL is used when looking at all atom positions (the other [<span class="underline">90%</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2877634/) of the protein).

What is a good RMSD? There doesn’t seem to be a strict answer and it’s a bit like comparing apples (accuracy) to oranges (resolution), but *in silico* models aim for a Cα-RMSD smaller than [<span class="underline">2.5 Å</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2286547/) (for reference X-ray crystallography is high resolution at \< [<span class="underline">3 Å</span>](https://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/resolution)).

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image34.png)
*[<span class="underline">Electron density maps for tyrosine 103 from myoglobin at 1.0 Å, 2.0 Å, and 2.7 Å resolutions, and tyrosine 130 from hemoglobin (chain B) at 3.0 Å resolution. The blue and yellow contours surround regions of high electron density, and the atomic model is shown with sticks.</span>](https://pdb101.rcsb.org/learn/guide-to-understanding-pdb-data/resolution)*

In the first ten years of CASP, the technique that made the most rapid [<span class="underline">progress</span>](https://onlinelibrary.wiley.com/doi/full/10.1002/prot.25800) was TBM. Progress has slowed in the following 8 years when many attempts to improve on the best template ironically turned it into a [<span class="underline">worse</span>](https://pubmed.ncbi.nlm.nih.gov/16187345/) model. Fortunately, there have been [<span class="underline">substantial improvements</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5820169/) recently with average precision increasing from 27% in CASP211 (2014) to 47% in CASP12 (2016), in part due to improved understanding of the energetics of protein folding but also largely by taking advantage of the growing databases.

As for FM, The first time anyone got it [<span class="underline">remotely right</span>](https://onlinelibrary.wiley.com/doi/10.1002/\(SICI\)1097-0134\(1999\)37:3+%3C194::AID-PROT24%3E3.0.CO;2-F) was around CASP3 (1998), and the subsequent [<span class="underline">progress</span>](https://www.nature.com/articles/s41467-019-11994-0) has mostly just been on small, single-[<span class="underline">domain</span>](https://www.wikiwand.com/en/Protein_domain) proteins, but hey at least there is [<span class="underline">progress</span>](https://onlinelibrary.wiley.com/doi/pdf/10.1002/prot.25423).

One of the factors that lead to the recent breakthrough of FM is residue‐residue [<span class="underline">coevolutionary analysis</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3233603/) as demonstrated in 2014 [<span class="underline">CASP11</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4834069/) and 2016 [<span class="underline">CASP12</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5820169/). You can narrow down the search space when you realise that when one amino acid mutates to be positively charged, another amino acid must mutate to be negatively charged for the two amino acids to keep in contact during evolution.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image27.png)
*[<span class="underline">Coevolution</span>](https://zenodo.org/record/1405369)*

Another factor is deep learning which was [<span class="underline">introduced</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3509494/) into the field in 2012 and demonstrated as the best method for protein contact prediction in 2012 CASP10. There was significant [<span class="underline">improvement</span>](https://pubmed.ncbi.nlm.nih.gov/29139163/) in 2016 CASP 12 where convolutional neural networks, residual networks, coevolutionary analysis, fragment assembly, and distance geometry were combined to build protein structural models from scratch.

## Top Dogs

One of the consistently [<span class="underline">top-ranking</span>](https://zhanglab.ccmb.med.umich.edu/I-TASSER/) servers in CASP is [<span class="underline">I-TASSER</span>](https://www.wikiwand.com/en/I-TASSER) (as Zhang-Server) developed by the [<span class="underline">Yang Zhang Lab</span>](https://zhanglab.ccmb.med.umich.edu/research/#StructurePrediction) at the University of Michigan. It uses threading and Monte Carlo simulations based on fragments.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image12.png)
*[<span class="underline">Flowchart of I-TASSER</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6407873/)*

Another top-ranking server is [<span class="underline">Rosetta</span>](https://www.rosettacommons.org/software) developed by the [<span class="underline">David</span>](https://www.wikiwand.com/en/David_Baker_\(biochemist\)) [<span class="underline">Baker Lab</span>](https://www.bakerlab.org/) at the University of Washington. It is optimised for predicting the tertiary structure of single protein domains, with the first step usually being domain parsing (or domain boundary prediction) to first split a protein into potential structural domain using Monte Carlo simulation. After the structures of individual domains are predicted, they are docked together in domain assembly to form the final tertiary structure. Rosetta was released as [<span class="underline">Rosetta@home</span>](https://boinc.bakerlab.org/) to use idle computer processing resources from volunteers' computers to perform calculations. Baker lab also released [<span class="underline">Foldit</span>](https://www.wikiwand.com/en/Foldit), an online protein structure prediction game based on the Rosetta platform. As of March 28 2020, Rosetta@home had 54,800 computers providing an average performance of over [<span class="underline">1.7 PetaFLOPS</span>](https://www.boincstats.com/stats/14/project/detail/) (10<sup>15</sup> FLOPS). Despite huge computing power even back in 2007, it took almost 2 years and 70,000 home computers to [<span class="underline">predict</span>](https://www.nature.com/articles/nature06249) the tertiary structure of the protein T0283 from its amino acid sequence. Rosetta@home’s highest achievement was correctly predicting the structure of a 256 amino acid long sequence in CASP11.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image30.png)
*[<span class="underline">Overview of Rosetta’s protocol in the CASP13 NMR-assisted structure prediction category.</span>](https://www.biorxiv.org/content/10.1101/597724v1.full)*

What about Stanford's [<span class="underline">Folding@home</span>](https://www.wikiwand.com/en/Folding@home) (FAH)[^4]? It's probably the better known distributed computed project. The conformational states from Rosetta's software can be used to initialize a Markov state model as starting points for FAH simulations. FAH almost exclusively uses all-atom molecular dynamics models to understand how and why proteins fold. As far as I know, it has never competed in CASP.

DeepMind debuted in CASP13 (2018) with [<span class="underline">Alpha Fold</span>](https://www.nature.com/articles/s41586-019-1923-7.epdf?author_access_token=Z_KaZKDqtKzbE7Wd5HtwI9RgN0jAjWel9jnR3ZoTv0MCcgAwHMgRx9mvLjNQdB2TlQQaa7l420UCtGo8vYQ39gg8lFWR9mAZtvsN_1PrccXfIbc6e-tGSgazNL_XdtQzn1PHfy21qdcxV7Pw-k3htw%3D%3D) and came first in overall performance with a sum [<span class="underline">Z-score</span>](https://www.wikiwand.com/en/Standard_score) (the difference of a sample’s value with respect to the population mean, divided by the standard deviation) of 128.07. The top groups, especially the Baker and Zhang groups, are often running neck and neck, so DeepMind really proved themselves to be the α-ML by doing the best for 1/3 of targets. It was a bit [<span class="underline">overhyped</span>](https://blogs.sciencemag.org/pipeline/archives/2018/12/03/the-latest-on-protein-folding) though, as the result is ultimately within the bounds of the usual expectations of academic progress, albeit at an accelerated rate. The [<span class="underline">data</span>](https://predictioncenter.org/casp13/zscores_final.cgi) shows that it often [<span class="underline">outperforms</span>](https://predictioncenter.org/casp13/gdtplot.cgi?target=T0965-D1&group=142&models=first) everyone else, but other times it just [<span class="underline">wanders off</span>](https://predictioncenter.org/casp13/gdtplot.cgi?target=T0966-D1&group=142&models=first) (which happens to every program).

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image17.png)
*[<span class="underline">There is only room for one at the top (left-most).</span>](https://predictioncenter.org/casp13/zscores_final.cgi)*

## AlphaFold 2: Electric Boogaloo

**<span class="underline">6.1 Results</span>**

Just when you thought AlphaFold was impressive, its sequel blew away everyone else with a 244 sum Z-score. Note that these are single proteins, not categories like multimeric complexes where DeepMind did not participate.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image13.png)
*[<span class="underline">I can't even see any of you from up here.</span>](https://predictioncenter.org/casp14/zscores_final.cgi?formula=gdt_ts)*

If you think the relative performance is astounding, the improvement in actual performance across the board is nothing short of staggering. AF2 achieved a median score of 92.4 GDT overall across all targets, and a median score of 87.0 GDT in FM. As seen in the graph below, AF2 is able to predict structures with GDT\_TS of almost 90 when the next best method only achieves a GDT\_TS of 20 (nonsense), and even GDT\_TS of above 90 and 95 in some cases when the next best method only achieve a (good) score of about 80.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image38.png)
*[<span class="underline">The delta between AF2 and the next best method this year.</span>](https://moalquraishi.wordpress.com/2020/12/08/alphafold2-casp14-it-feels-like-ones-child-has-left-home/)*

You can’t deny the magnitude of the breakthrough:

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image35.png)
[<span class="underline">Combined results of all the CASP competitions. The dark orange line (CASP14\_serv) corresponds to the predictions made by fully automated servers, the olive green line (CASP14\_w/o427) includes all predictions assisted by humans except for the highest performing group; and the black line (CASP14) represents the predictions by the best performing team: Group 427, or AF2.</span>](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/?s=09)

AF2 achieved a mean RMSD of about 1.6Å, and \<5Å 92.5% of the time over all side chain atoms. it achieves RMS\_CA of \<1Å 25% of the time, \<1.6Å 50% of the time, and \<2.5Å 75% of the time. In terms of RMS\_All, it achieves \<1.5Å 25% of the time, \<2.1Å 50% of the time, and \<3Å 75% of the time.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image16.png)

*[<span class="underline">Distribution of RMSDs for the highest-ranked models submitted by AlphaFold 2.</span>](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/?s=09)*

Some results from AF2 are so good that they defied the experimentally determined models. For example, [<span class="underline">Osnat Herzberg</span>](http://www.chem.umd.edu/faculty-staff-directory/facultydirectory/osnat-herzberg)’s group, who were studying a phage tail protein, noticed that they had a different assignment for a cis-proline compared to the model from AF2. Upon reviewing the analysis, they realised they had made a mistake in the interpretation and [<span class="underline">corrected</span>](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/?s=09) it. Another example is [<span class="underline">Henning Tidow</span>](https://www.chemie.uni-hamburg.de/en/institute/bc/arbeitsgruppen/tidow/personen/tidow-henning.html)’s group, who were trying but struggling to perform X-ray crystallography on an integral membrane protein, reductase FoxB (related to iron uptake in Gram-negative bacteria) for about two years. When they saw the models from AF2, they managed to solve the problem by [<span class="underline">molecular replacement</span>](https://www.wikiwand.com/en/Molecular_replacement#:~:text=Molecular%20replacement%20\(or%20MR\)%20is,the%20diffraction%20data%20is%20derived.) in a matter of hours.

**<span class="underline">6.2 A closer look thanks to [Carlos Outeiral Rubiera](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/?s=09)</span>**

DeepMind highlighted the [<span class="underline">ORF8</span>](https://www.biorxiv.org/content/10.1101/2020.08.27.270637v1) protein (labelled as T1064 in CASP14; 7JTL in PBD), a viral protein involved with the interaction between SARS-CoV-2 and the immune response, as one of the targets “where they didn’t do that well”.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image7.png)

*[<span class="underline">AF2 model for the T1064 target (red), superimposed onto the 7JTL\_A structure (blue).</span>](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/?s=09)*

AF2’s model of the core of the protein is in excellent agreement with the experimental structure, down to the antiparallel β-sheets, and more impressively, the loops (top and right) that connect them. As for the large loop region (bottom left) that looks very different from the experimental structure, it does bear some resemblance to the actual loop, and its performance is still better than most common methods. Also, loop regions are commonly very flexible, so it can just mean that that region is mobile. [<span class="underline">Apparently</span>](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/?s=09), a new experimental structure of the ORF8 protein actually displays a much similar structure to the prediction. Loops are generally considered hard to predict, and compared to usual methods, AlphaFold 2’s performance is quite impressive.

How did the Zhang and Baker groups do?

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image28.png)
*[<span class="underline">Top: highest-ranked models for the target T1064 submitted by the Zhang (black) and Baker (green) human groups. Bottom: models aligned with the crystal structure. Right: all three models (Zhang, Baker and AlphaFold 2) aligned with the crystal structure.</span>](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/?s=09)*

It’s pretty clear that AF2 is in a class of its own. Zhang’s group barely captures the structure of the core, while Baker’s group shows more β-sheets than the crystal structure and the topology falsely combines parallel and antiparallel sheets. In both cases, the loops connecting the β-sheets are all around the place, and the large 30-residue loop region that AF2 didn’t model correctly is modelled even worse by these two submissions.

What about models where DeepMind acknowledges that it did really well? Let’s look at the target T1046s1 (6x6o chain A, in PDB).

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image19.png)

*[<span class="underline">AF2 model for the T1046s1 target (red), superimposed onto the 6X6O\_A structure (blue).</span>](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/?s=09)*

The AF2 model, especially the α-helices and the loops, is virtually indistinguishable from the crystal structure with a total RMSD of 0.48Å.

In fact, the agreement is so good that it extends to side chains:

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image15.png)
*[<span class="underline">AlphaFold 2 not only predicts the global structure of the protein with high accuracy — it also produces incredibly accurate forecasts of the side chain structure</span>](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/?s=09)*

How did the Zhang and Baker groups do?

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image32.png)
*[<span class="underline">Top: highest-ranked models for the target T1046s1 submitted by the Zhang (black) and Baker (green) human groups. Bottom: models aligned with the crystal structure (blue). Right: all three models (Zhang, Baker and AlphaFold 2, red) aligned with the crystal structure (blue).</span>](https://www.blopig.com/blog/2020/12/casp14-what-google-deepminds-alphafold-2-really-achieved-and-what-it-means-for-protein-folding-biology-and-bioinformatics/?s=09)*

While the Zhang and Baker models are very good, close examination reveals some discrepancies. The kink in the first α-helix is not reproduced accurately: Zhang’s group models it as an essentially straight helix, while Baker groups shows a smaller kink. In comparison, AF2 modelled the kink to perfect accuracy. Also, the magnitude of the deviations is a lot larger than that in the AF2 model.

## How Did DeepMind Do It?

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image36.png)
[<span class="underline">Overview of AF2 architecture</span>](https://deepmind.com/blog/article/alphafold-a-solution-to-a-50-year-old-grand-challenge-in-biology)

Unfortunately, DeepMind hasn’t published a paper on AF2 yet, so we can only guess.

The current standard (also used by AlphaFold the first) is to extract summary coevolutionary statistics from a [<span class="underline">multiple sequence alignment</span>](https://www.wikiwand.com/en/Multiple_sequence_alignment) ([<span class="underline">MSA</span>](https://journals.aps.org/pre/abstract/10.1103/PhysRevE.87.012707)) of homologous protein sequences, then fed into a neural network to predict a “distogram”: a matrix of the probabilities of pairwise distances between all Cβ atoms. This distogram acts as a constraint to narrow the configuration space significantly. MSAs can often be noisy, containing sequences that are not evolutionary related.

DeepMind reformulates the entire pipeline to be end-to-end differentiable; instead of using the MSA to predict distogram constraints, their architecture takes the raw MSA as input and outputs a full structure at the end:

1. [<span class="underline">Attention model</span>](https://towardsdatascience.com/attention-in-neural-networks-e66920838742?gi=b0c6090086c5): AF2 decides which raw sequences to look at and which noisy ones to ignore, and from that predicts a distogram, upon which it decides which sequences to attend to next, and so on for a few hundred iterations
    
   - Leverages deeper (as in having more sequences) MSAs for individual protein domains/intra-domain details, and shallower ones for whole proteins/inter-domain details
       
   - It [<span class="underline">doesn’t</span>](https://twitter.com/d_kihara/status/1335631335759745034?s=20) even explicitly use co-evolution\!

2. After some number of iterations, AF2 generates a 3D atom cloud from the distograms that is then fed into a transformer for 10 iterations
    
   - Captures higher-order coordinations between more than 2 atom (information not captured by distograms)
       
   - It doesn’t use any physics simulation\!

3. In a few hundred iterations, AF2 begins building the local structure within individual protein domains before branching out to more global features, and outputs a full structure at the end.
    
   - It ensures self-consistency at every step of the pipeline, as traditionally distances between all atoms are first predicted simultaneously (can be nonsense if not embedded in 3D space) then optimised (sometimes physics-based)

4. In TBM, AF2 takes homologues directly as inputs along with the MSA
    
   - But AF2 was also able to perform well in FM

## Why DeepMind?

Of course we know that AF2 couldn’t have been invented in a vacuum, but it is especially true as AF2’s attention model uses existing sequences most thoroughly. AF2 is built on all the previous work done by academics, including the whole body of research in peer-reviewed articles, the software tools developed by academic prediction groups, and data painstakingly collected by structural biology groups for decades. Many of the ideas that AF2 incorporates, such as using MSA and templates, all come from the prior research conducted, written up, and reviewed by academics, funded by public money. Also, AF2 is trained using the ~170,000 structures from the PDB and data from the UniRef, as well as data from the BFD and MGnify databases of metagenomics sequences. Moreover, AF2 uses software tools like HHblits, JackHMMER and OpenMM that were developed by academics. DeepMind managed to see further because they stood on the shoulders of giants.

Other than prior work by academics, DeepMind’s success has come as a surprise as no one expected it to come [<span class="underline">so soon</span>](https://www.nature.com/articles/d41586-020-03348-4). The novel approach in AF2 and the brilliant engineering can be attributed to 2 reasons why it wasn’t an academic group that solved protein structure prediction.

First, DeepMind has unlimited computing power thanks to unlimited money. Tensor Processing Units (TPUs) are a proprietary Application-Specific Integrated Circuit (ASIC) developed by Google from the ground up for deep learning, unlike GPUs that were originally designed to process graphics. For example, an 8-core TPU v3 chip has 128 GB of vRAM (necessary for high memory-cost attention models like AF2), while an NVIDIA A100 (the GPU with the largest RAM as of writing) “only” has 40 GB. Deepmind says that it uses approximately 16 TPUv3s (which is 128 TPUv3 cores or roughly equivalent to ~100-200 GPUs) run over a few weeks, and renting 128 TPUv2 cores has an annual cost of half a million dollars as per Google Cloud’s pricing page, so AF2’s total computational cost is likely to be in the region of several million dollars. Meanwhile, the Baker and Zhang groups said they used around 4 GPUs for a couple of weeks. This means the AF2 team had roughly two orders of magnitude more computational resources than even the best funded academic research groups.

Interestingly, although DeepMind says that AF2 uses a “relatively modest” amount of compute in the context of most large state-of-the-art machine-learning models, it is in fact an insane amount given that they are not doing any MD.

AlQuraishi says,

> “Nothing in their architecture as I understand it could warrant this much compute, unless they’re initializing from multiple random seeds for each prediction. The most computationally intensive part is likely the iterative MSA/distogram attention ping-pong, but even if that is run for hundreds or thousands of iterations, the inference compute seems too much. MSAs can be very large, that is true, but I doubt that they’re using them in their entirety as that seems overkill.”

Vast computational resources doesn’t only allow DeepMind to use mysterious, large models, it also allows a much higher throughput than any academic group. What the Baker group needed a month to test in their 4 Titan GPUs might only take a few hours for DeepMind, allowing for rapid prototyping and testing of ideas.

Second, organisational structure is another key factor beyond unsubstitutable individual contributors. At DeepMind, professionals in the same job with deep expertise spend most of their time doing research, all coordinated in the single direction of building AF2 (which has 18 co-first authors). In academic labs, there are a lot of administrative tasks that take up a lot of time that could’ve been spent doing research, and the constant turnover of students and postdocs means shallower expertise with limited collaboration because at the end of the day it’s about individual effort and building a personal brand. It’s all about the incentives\!

However, as AlQuraishi cautions, it would be short-sighted to turn the entire research enterprise into many mini DeepMinds. Unlike protein structure prediction (which literally has a leaderboard every 2 years), most of biology doesn’t have well-defined questions, and the academic model is much better at asking questions, while the DeepMind is only better at answering them. More subtly, the fast and focus model means that there is ironically less time for idea exploration and for new ideas to gestate into the literature to inform questions even beyond protein structure prediction. Once a solution is solved in any way, it becomes hard to justify solving it another way, especially from a publication standpoint. At least for now, we can kind of have our cake and eat it too when fast and focused efforts co-exist with the slow and steady progress of conventional research.

## Wait, So Is The Protein Folding Problem Solved?

Again, the [<span class="underline">protein-folding problem</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2443096/#:~:text=The%20protein%20folding%20problem%20is,first%20atomic%2Dresolution%20protein%20structures.) came to be three main questions:

1. *The physical folding code*: How is the 3D native (properly-folded/functional) structure of a protein determined by the physicochemical properties that are encoded in its 1D amino-acid sequence?

2. *The folding mechanism*: A polypeptide chain has an almost unfathomable number of possible conformations. How can proteins fold so fast?

3. *Predicting protein structures using computers*: Can we devise a computer algorithm to predict a protein’s native structure from its amino acid sequence?

Obviously, AF2 has almost no (direct) bearing on the first 2 questions regarding the actual dynamic folding pathways. So I don’t think it’s controversial to say that DeepMind [<span class="underline">has not</span>](https://foldingathome.org/2020/12/08/protein-folding-and-related-problems-remain-unsolved-despite-alphafolds-advance/) solved the protein folding problem per se, but has it solved protein structure prediction? It is itself an umbrella term for distinct problems of predicting:

1. the structure of a single protein domain from sequence,

2. the structure of a single protein, possibly comprised of multiple domains, from sequence,

3. the structure of a multimeric complex,

4. the major conformations of a protein.

For each of the above, there are additional questions:

- *“Purity” of solution*: was the prediction made from just a single sequence, or was it made using additional information like homologous protein sequences, homologous structures, and even other forms of non-sequence-based experimental data?

- *Scope of solution*: Does a solution need to address all of the corner cases and elaborations e.g. proteins containing metals and other co-factors, unnatural amino acids, entirely de novo proteins?

- *Accuracy*: how good is good enough?

Well, AF2 reliably (\>90% of the time) predict to reasonable accuracy (\<3-4Å) the lowest energy structure of vanilla (no co-factors, no obligate oligomerisation) single protein chains using a list of homologous protein sequences from the PDB (well-known to be biased towards proteins that are easily crystallised).

The list of [<span class="underline">caveats</span>](http://occamstypewriter.org/scurry/2020/12/02/no-deepmind-has-not-solved-protein-folding/) is a long one, but whether DeepMind solved protein structure prediction can be a bit of a motte (a general solution) and bailey (a universal solution). I think it’s useful to phrase the question as whether we can devise a computer algorithm to predict a protein’s native structure from its amino acid sequence. Since we did not know the answer before AF2 came out, and now we do know that a solution is possible, AF2 counts as a solution, which seems like the consensus among experts like AlQuraishi anyway. The core scientific question of prediction *in silico* has been answered, so the remaining problems are now engineering rather than scientific (not that engineering problems are any easier or less important).

## What Are The Implications?

Mostly a rehash of AlQuraishi’s [<span class="underline">speculations</span>](https://moalquraishi.wordpress.com/2020/12/08/alphafold2-casp14-it-feels-like-ones-child-has-left-home/), do read his essay for more.

**<span class="underline">Protein structure prediction</span>**

AlQuraishi again,

> ”The core field has been blown to pieces; there’s just no sugar-coating it. I can say this because it’s (one of) my own field(s). There are some intellectually interesting exercises left, for example predicting structure from a single sequence without structural templates or evolutionary information, and there are important engineering problems including addressing all the corner cases that AF2 still can’t. These are important and scientifically worthwhile but will be of limited interest beyond the core community of structure predictors.“

**<span class="underline">Experimental structure biology</span>**

As mentioned above, in the most immediate term, AF2 has already helped X-ray crystallography. However, beyond the short-term (\>3-5 years) AF2 will begin to undercut demand for X-ray crystallography as there are a myriad of applications in biology that will benefit from having structures at 3Å or 4Å accuracy that is not as high as X-ray crystallography.

An important caveat is that AF2 is trained on crystallography structures from the PDB, but because cell cytoplasm is not crystal, most crystallized protein structures are probably not particularly good representatives of physiologic state\! In the future when other experimental techniques and physics-based computational methods are systematically integrated, we may get predicted structures that would be more informative than crystal structures in determining a protein’s biological function.

What about single particle CryoEM? It has a better short to medium outlook as it is increasingly focused on quaternary complexes and molecular machines, where AF2 can help CryoEM with resolving individual monomers. Still, DeepMind has made it clear that complexes are their next big target, so we will have to see what happens.

The one area that will remain safe and wholly complementary to AF2 is in situ structural biology, because AF2 cannot determine the cellular context of proteins. If anything, AF2 may accelerate the breakneck pace of progress in CryoET and usher in the era of structural cell biology faster than even its proponents are expecting.

## Will It Revolutionise Drug Discovery?

No. At least [<span class="underline">not</span>](https://www.nature.com/articles/d41586-018-05267-x) in the near term.

AF2’s predictions are still not accurate enough to deliver reliable insights into protein chemistry or drug design, which will require accuracy of around 0.3 Å. AF2’s best prediction has an RMSD for all atoms of 0.9 Å. The average RMSD of AF2’s 111 predictions is 1.6 Å (about the size of a bond-length), which is very [<span class="underline">impressive</span>](https://blogs.sciencemag.org/pipeline/archives/2020/11/30/protein-folding-2020) but still not sub-angstrom.

That said, AF2 might be able to help in determining structures of protein targets that can be modulated for therapeutic purposes designing protein-based (e.g. antibodies and peptides), where ultra-high accuracy is less needed. The challenge is that AF2 is trained to predict apo (unbound) protein structures while most medicinal chemistry applications require complexes of the protein bound to a small molecule.

But in any case, protein structure determination simply isn’t a rate-limiting step in drug discovery in general, not even if X-ray crystallography were to become fast and routine. If you have a solid primary assay against a target you really believe in, and an animal model with real translatability, you don’t need a defined target to get a drug to market. What you absolutely need are safety and efficacy data from successful human clinical trials which require the FDA to allow your IND application. The best way to get an IND approved is to show activity in a relevant animal model and clean toxicology studies in at least two species, and you can do those without knowing the protein target at all, let alone its structure.

The [<span class="underline">biggest challenge</span>](https://blogs.sciencemag.org/pipeline/archives/2020/12/01/the-big-problems) of drug discovery is choosing the wrong target, because our understanding of biology just isn't there yet, and we can only speculate about how much impact protein structure determination will have on that. So many compounds fail in human trials because turns out our hypothesis about the underlying pathophysiology was just wrong[^6].

One class of disease where protein structure determination might help us understand better is [<span class="underline">proteopathy</span>](https://www.wikiwand.com/en/Proteopathy#/list_of_proteopathies) that is caused by protein misfolding.[^8] Take Alzheimer's disease for instance, while its exact cause remains unknown, it is [<span class="underline">associated</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2274891/) with toxic aggregations of the misfolded amyloid beta (Aβ) peptide that grows into significantly larger senile plaques. As these [<span class="underline">aggregates</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3837440/) are heterogeneous, experimental methods such as X-ray crystallography and nuclear magnetic resonance (NMR) have had difficulty determining their structures. It doesn’t help that atomic simulations of Aβ aggregation are very [<span class="underline">computationally demanding</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2674793/) due to their size and complexity.

> ![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image9.jpg)![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image33.jpg)![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image23.jpg)

*[Toxic aggregations of the misfolded Aβ peptide in Alzheimer’s disease.](https://en.wikipedia.org/wiki/Alzheimer%27s_disease?oldformat=true#Biochemistry)*

Another example is [<span class="underline">prion</span>](https://www.wikiwand.com/en/Prion)<sup>1</sup>, an exception to Anfinsen's dogma as it is a stable conformation that differs from the native folding state. The misfolding of normal prion protein (PrPc) into prototypical prion disease–scrapie (PrPSc) causes a host of proteopathies known as [<span class="underline">transmissible spongiform encephalopathies</span>](https://www.wikiwand.com/en/Transmissible_spongiform_encephalopathy) (TSEs) such as [<span class="underline">Bovine spongiform encephalopathy</span>](https://www.wikiwand.com/en/Bovine_spongiform_encephalopathy) (Mad Cow Disease), [<span class="underline">Creutzfeldt-Jakob disease</span>](https://www.wikiwand.com/en/Creutzfeldt%E2%80%93Jakob_disease) and [<span class="underline">fatal insomnia</span>](https://www.wikiwand.com/en/Fatal_insomnia). TSEs are especially scary because the ‘seeding’ of the infectious PrPSc, arising spontaneously, hereditary or via contamination, can cause a chain reaction of transforming normal PrPc into fibrils aggregates or amyloid like plaques consisting of PrPSc. The molecular structure of PrPSc has not been fully characterised due to its aggregated nature. Neither is known much about the mechanism of the protein misfolding nor its kinetics.

AF2 may give us some insights into proteopathies if we can analyse how the neural network infers the folded structure, but that can be even harder than protein folding (neural nets are black boxes), and even if we manage to it might also be useless simply because the network’s inference is just not very representative of the dynamic folding process.

Better models (animal and otherwise) of such diseases and conditions would be helpful too, but that also depends on how much we know about underlying pathophysiology. For example, the underlying difficulty of countless compounds for Alzheimer’s that work in animal models but fail in human trials is that humans are the only animal that actually gets Alzheimer’s. It’s a chicken-and-egg question; you would need to know a lot more about the disease before you can create a good model.

In the long run, the true power of AF2 may come in providing a more robust platform for discovery drugs based on their polypharmacology i.e. to modulate multiple protein targets intentionally, which may be able to modulate entire signaling pathways instead of acting on one protein at a time. There’s a lot more work to be done, but in the meantime, we can appreciate that AF2 is one of the most significant scientific breakthroughs in our lifetime.

## Endnotes

[^7]: [<span class="underline">One</span>](https://philosophy-science-humanities-controversies.com/listview-details.php?id=2632820&a=$a&first_name=Eliezer&author=Yudkowsky&concept=AI%20Takeover) of [<span class="underline">Eleizer Yudkowsky's</span>](https://twitter.com/ESYudkowsky/status/1333450511064842247?s=20) scenarios of AI takeover:

    1. Crack the protein folding problem to the extent of being able to generate DNA strings whose folded peptide sequences fill specific functional roles in a complex chemical interaction.

    2. Email sets of DNA strings to one or more online laboratories that offer DNA synthesis, peptide sequencing, and FedEx delivery.

    3. Find at least one human connected to the Internet who can be paid, blackmailed, or fooled by the right background story, into receiving FedExed vials and mixing them in a specified environment.

    4. The synthesized proteins form a very primitive “wet” nanosystem, which, ribosome-like, is capable of accepting external instructions; (…)

    5. Use the extremely primitive nanosystem to build more sophisticated systems, which construct still more sophisticated systems, bootstrapping to molecular nanotechnology—or beyond.

[^1]: Proteins are chains of amino acids joined together by peptide bonds. The many 3D conformations of this chain are possible due to the rotation of the chain about each [<span class="underline">alpha carbon</span>](https://www.wikiwand.com/en/Alpha_and_beta_carbon) (Cα) atom, the backbone carbon before the carbonyl carbon atom in the protein molecule. So what [<span class="underline">forces</span>](https://www.sciencedirect.com/science/article/abs/pii/S0022283607007371?via%3Dihub) [<span class="underline">drive</span>](https://www.sciencedirect.com/science/article/abs/pii/S0022283607007371?via%3Dihub) the rotation of the amino acid chains? Some are:

    - *Hydrogen bonds*: α-helix and β-sheet were predicted by Linus Pauling from hydrogen-bond models

    - *van der Waals interactions*: duh

    - *Backbone angle preferences*: polymers have preferred angles of neighbouring backbone bond orientations

    - *Electrostatic interactions*: some amino acids attract or repel because of negative and positive charges

    - *Hydrophobic interactions*: proteins ball up with the hydrophobic amino acids in the core and the polar amino acids on the surface

    - *Chain entropy*: opposing the folding process is a large loss in chain entropy as the protein collapses into its compact native state from its many open denatured configurations

    Through statistical mechanical modelling in the 1980s, minimising the number of hydrophobic side-chains exposed to water, or the [<span class="underline">hydrophobic effect</span>](https://www.sciencedirect.com/topics/chemistry/hydrophobic-effect), has been shown to be the predominant [<span class="underline">driving force</span>](https://www.pnas.org/content/113/44/12462) behind the folding process. An ordering of water molecules around a hydrophobic region (“water cage”) contributes a negative change in entropy. The hydrophobic collapse (inward folding of the hydrophobic groups) introduces entropy back to the system via the breaking of the “water cages” which frees the ordered water molecules. The multitude of hydrophobic groups interacting within the core of the folded protein significantly contributes to protein stability after folding due to the vastly accumulated van der Waals forces.

    ![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image11.png)
    *[Hydrophobic collapse: in the compact fold (to the right), the hydrophobic amino acids (shown as black spheres) collapse toward the center to become shielded from aqueous environment.](https://www.wikiwand.com/en/Hydrophobic_collapse)*

    Currently, we don’t fully understand the energetic processes and tradeoffs in folding any given protein, but this field of energetics in protein folding is [<span class="underline">advancing</span>](https://www.nature.com/articles/srep24035). At the end of the day, we still haven't found sequence patterns, say of hydrophobic, polar, charged, and aromatic amino acids, that would predict protein structures and stabilities. So the first question of the protein folding problem remains unsolved.

[^2]: See my [post](https://subcriticalappraisal.com/2020/Solution-To-Levinthals-Paradox/) about Levinthal's paradox. It has a solution!

[^3]: [<span class="underline">Anfinsen's dogma</span>](https://www.wikiwand.com/en/Anfinsen%27s_dogma) (a.k.a. the [<span class="underline">thermodynamic hypothesis</span>](https://science.sciencemag.org/content/181/4096/223)) postulates that the native structure of a protein is its most thermodynamically stable structure; it depends only on the amino acid sequence and on the conditions of solution, and not on the kinetic folding route.

    Keeping in mind that systems tend to move towards its global free energy (energy available in a system to do useful work) minimum, there are three conditions:

    1. **Uniqueness**: the free energy minimum must be unchallenged; the sequence does not have any other configuration with a comparable free energy

    2. **Stability**: small changes in the surrounding environment cannot give rise to changes in the minimum configuration; the free energy surface around the native state must be rather steep and high, in order to provide stability

    3. **Kinetical accessibility**: the path in the free energy surface from the unfolded to the folded state must be reasonably smooth; the folding of the chain must not involve highly complex changes in the shape (e.g. knots)

    Put simply, to determine a protein's native structure, all the information you need is in its amino-acid sequence<sup>2,3</sup>. But at the end of the day, we still haven't found sequence patterns, say of hydrophobic, polar, charged, and aromatic amino acids, that would predict protein structures and stabilities. So the first question of the protein folding problem remains unsolved.

    ![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image25.png)
    *[<span class="underline">Anfinsen’s experiment.</span>](https://greatexperimentsblog.blogspot.com/2017/11/anfinsens-dogma.html)*

    Anfinsen [<span class="underline">demonstrated</span>](https://www.jbc.org/content/237/6/1839.full.pdf) it in his [<span class="underline">now</span>](https://www.jbc.org/content/236/5/1361.long)-[<span class="underline">famous</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC223141/?page=1) [<span class="underline">experiments</span>](https://www.jbc.org/content/237/6/1839.full.pdf) from 1960 to 1962 by using a protein called ribonuclease A (RNase A), which contains four disulfide bridges that are vital to protein structure and function. First, he unfolded RNase A with urea (which denatures or causes the loss of native structure of protein) and βME (a reducing agent that breaks disulfide bridges). When Anfinsen removed urea first and βME second, the protein refolded and regained 100% activity. However, when he removed βME first and urea second, the protein only regained 1% of its original activity. This was because removing βME when the enzyme is still unfolded causes cysteine (an amino acid) residues to randomly form disulfide bonds with each other.

    There are some caveats. Some proteins need the assistance of another protein called a chaperone protein which seems to work primarily by preventing aggregation of several protein molecules prior to the final folded state of the protein. It has been suggested that this disproves Anfinsen's dogma, but many chaperones do not appear to affect the final state of the protein.

[^4]: See my [post](https://subcriticalappraisal.com/2020/Charity-Is-Still-Not-About-Helping/) about Folding@home as a scientific lemon project running on high resource costs and why charity is still not about helping.

[^5]: There have been many attempts to get faster at doing these kinds of calculations. IBM’s (retired?) [<span class="underline">Blue Gene</span>](https://www.nature.com/articles/nbt0100_8d) supercomputers boasted of operating speeds in the petaFLOPS range with lower power consumption, but I couldn’t find any protein prediction paper from them at all, and it seems that they have ended development in 2015.

[^6]: [Another thing]((https://blogs.sciencemag.org/pipeline/archives/2020/12/01/the-big-problems)) that will speed up drug discovery is a better warning system for toxicity in human trials as well. Many promising drugs have dropped out of the clinic due to unexpected tox effects, for sure – some of these turn out to be mechanism-related and some of them are just compound-related (where the compound does something else that you don’t want), but there are many instances where we can’t even make that distinction yet. Animal models for toxicity are extremely valuable, but they don’t get you all the way. You are still taking a risk every time a new compound or new mechanism goes into human trials, and it would be very useful if we could lower that risk a bit. The general solution would be some sort of system that exactly mimics human biology but doesn’t consist of a bunch of human swallowing pills. This is a difficult goal to realize.

[^8]: In 2011, the European Medicines Agency [approved](https://www.nature.com/articles/nrd3675) the use of [Tafamidis](https://www.wikiwand.com/en/Tafamidis) a.k.a. Vyndaqel/Vyndamax (a kinetic stabilizer of tetrameric transthyretin) to delay peripheral nerve impairment in adults with [transthyretin amyloid diseases](https://www.wikiwand.com/en/Familial_amyloid_polyneuropathy). In 2019, the FDA [approved](https://www.fda.gov/news-events/press-announcements/fda-approves-new-treatments-heart-disease-caused-serious-rare-disease-transthyretin-mediated) Vyndaqel and Vyndamax for the treatment of transthyretin mediated cardiomyopathy. This suggests that the process of amyloid fibril formation (and not the fibrils themselves) causes the degeneration of post-mitotic tissue in human amyloid diseases.