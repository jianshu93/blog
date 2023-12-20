---
layout: post
title: Evaluation of ANI calculators for microbial genomes
---

The massive amount of metagenomic sequencing has created a challenge: tons of microbial genomes assembled and binned from environmental samples. To compare those genomes (or MAGs) to investigate genomic diversity, average nucleitide identity (or ANI) is the most widely used and reliable way to calculate genome identity. Alignment-based ANI calculators, e.g., OrthoANI or ani.rb (enveomics package) are too slow for a dozen of genomes. 
FastANI or the recent skani  represent important breakthroughs fo the field in terms of the underlying data structure and algorithms. Minimizer-Jaccard estimator, as in MashMap or fastANI, as a new data structure for finding homologuous seqeunces in genome pairs, is very efficient and accurate. Skani applies sparse chaining algorithm and can be even faster for high ANI values, but lose accuracy for ANI below 85% or so. I compare alignment-based ANI, ANIu (orthoANI based on Usearch) with fastANI and skani and found that skani, despite being fast for >85% ANI, has much large variation for 85% ANI or below. 

![_config.yml]({{ site.baseurl }}/images/ANIu_vs_FastANI.png)
Figure 1. FastANI vs ANIu (usearch) for 300 genomes.
![_config.yml]({{ site.baseurl }}/images/aniu_vs_skani.png)
Figure 2. skani vs ANIu (usearch) for the same 300 genomes.

As you may notice, for below 80% ANI, fastANI is also less accurate (larger ANI values than ANIu) but very small variation. It is very easy to apply a linear correction as shown, from the blue fitted line (fastANI vs ANIu) to red fitted line to accuractly approximate alignment-based ANI without any additional computations.
![_config.yml]({{ site.baseurl }}/images/fastANI_correction_new_arrow.png)
Figure 3. Linear correction of fastANI to approximate alignment-based ANI.

This idea will be applied in the newest version of fastANI, which will be available soon!
