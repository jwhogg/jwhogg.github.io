---
title: 'Causal Implicit GAN: Data Augmentation for Causal Discovery'
date: 2024-06-032T14:25:04+01:00
draft: false
# math: true
# katex: true
---

[Github 🔗](https://github.com/jwhogg/CIGAN)

My University dissertation research project, where I designed and trained a GAN model for data augmentation (generating new training samples for downstream models). I was very proud to receive a score of 83 on this disseration (high 1st).

<img src="/images/cigan.png" alt="A high-level overview of the CIGAN project" width="60%">

The data the GAN generates is intended for use on Causal Discovery models, an area where quality ground-truth datasets are hard to come by- making data augmentation a valuable technique.  The novel contribution of my project is that the GAN is designed to implicitly learn causal relations, which we hypothesise leads to more 'realistic' output data.

The GAN generates an adjacency matrix representing a causal graph
<img src="/images/causal_graph.png" alt="An example causal graph that CIGAN generated" width="80%">

I am very grateful to my superviosr Ramsay Taylor for his support during this project, and to Hristo Petkov for his invaluable expertise on his DAG-WGAN model.