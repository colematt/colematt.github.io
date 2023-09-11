---
layout: post
title: "Accepted Paper at WDFHC '22"
date:   2022-11-01 06:59:00 -0500
tags: [conferences, accepted work]
---

Our paper _A Security Analysis of Labeling-Based Control-Flow Integrity Schemes_ by David Demicco, Matthew Cole, Shengdun Wang and Aravind Prakash has been accepted at [Workshop on Data Fabric for Hybrid Cloud 2022 (WDFHC '22)](https://hipc.org/wdfhc/).

<!--more-->

```bibtex
@INPROCEEDINGS{10056531,
  author={Demicco, David and Cole, Matthew and Wang, Shengdun and Prakash, Aravind},
  booktitle={2022 IEEE 29th International Conference on High Performance Computing, Data and Analytics Workshop (HiPCW)}, 
  title={A Security Analysis of Labeling-Based Control-Flow Integrity Schemes}, 
  year={2022},
  volume={},
  number={},
  pages={47-52},
  abstract={Secure and transparent policy enforcement by a cloud provider is crucial in cloud infrastructures. Particularly, enforcement of control-flow integrity (CFI) policy has been widely accepted for stopping software-induced attacks. Using low-level hardware metadata to encode CFI policy is a fairly recent development. Besides moving enforcement out of the software and into the hardware for performance benefit, tagging metadata also offers other benefits in the precision of defenses. We evaluate several different metadata layouts for CFI policy enforcement, and examine the layouts' effects on the number of valid forward edges remaining in a RISC-V binary after policy enforcement. Additionally we look at related work in tag-based tools that provide CFI policy enforcement in order to get a sense of their performance and the design trade-offs they make. We evaluate our policy and the related works in terms of space and precision trade-offs for forward- and backward-edge CFI, finding that some trade-offs have a higher impact on the number of remaining forward edges, notably return address protection. Additionally, we report that existing backward edge protections can be highly effective, reducing the number of remaining backward edges in a protected binary to an average of 0.034% over an equivalent coarse-grained CFI.},
  keywords={},
  doi={10.1109/HiPCW57629.2022.00011},
  ISSN={},
  month={Dec},}
```
