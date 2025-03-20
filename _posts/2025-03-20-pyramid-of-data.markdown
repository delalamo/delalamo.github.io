---
layout: post
title:  "Data breakpoints"
date:   2025-03-20 1:38:00
categories: [Metanotes]
---
PDB structures continue to be fenced off from where they're needed most.

The vast majority of publications are downloadable as PDFs and render images as static PNGs or equivalent file formats. That was understandable thirty years ago, as web technologies were not nearly as advanced as they are now. Yet even today, publications routinely host data on other sites, such as Zenodo, in a way that fully disconnects them from the main text itself. This not only adds unnecessary steps to data verification and reproducibility, but in some cases actively impedes readers from potentially getting a full picture of the research.

Here's one example for structural biologists: protein structures are almost always available for free on RCSB, but manuscripts always feature static pictures of them.

Here's Figure 8 from [a recent paper](doi.org/10.1016/j.str.2024.12.010) that shows an example:

![Figure 8A showing PDB 8SVE](/assets/post_images/2025_03_20/2025_03_20_A.png)

In contrast, compare this to directly uploading and visualizing the PDB in the web itself:

{% include 8sve.html %}
<div style="height: 640px;"></div>

In this case, since deposition of structures upon publication is standard practice, there is virtually no added effort on the part of the publications. The tweaks and optimizations that authors would need to do to make the pictures pretty are done in the viewer rather than in PyMol.