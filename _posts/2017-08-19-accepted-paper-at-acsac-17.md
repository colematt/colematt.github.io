---
layout: post
title:  "Accepted Paper at ACSAC '17"
date:   2017-08-19 17:29:00 -0500
tags: [conferences, accepted work]
---

Our paper _Supplementing Modern Software Defenses with Stack-Pointer Sanity_ by Anh Quach, Matthew Cole and Aravind Prakash has been accepted at [ACSAC '17](https://www.acsac.org/2017/).
The acceptance rate was 19.7%.

<!--more-->

```bibtex
@inproceedings{10.1145/3134600.3134641,
author = {Quach, Anh and Cole, Matthew and Prakash, Aravind},
title = {Supplementing Modern Software Defenses with Stack-Pointer Sanity},
year = {2017},
isbn = {9781450353458},
publisher = {Association for Computing Machinery},
address = {New York, NY, USA},
url = {https://doi.org/10.1145/3134600.3134641},
doi = {10.1145/3134600.3134641},
abstract = {The perpetual cat-and-mouse game between attackers and software defenders has highlighted the need for strong and robust security. With performance as a key concern, most modern defenses focus on control-flow integrity (CFI), a program property that requires runtime execution of a program to adhere to a statically determined control-flow graph (CFG). Despite its success in preventing traditional return-oriented programming (ROP), CFI is known to be ineffective against modern attacks that adhere to a statically recovered CFG (e.g., COOP).This paper introduces stack-pointer integrity (SPI) as a means to supplement CFI and other modern defense techniques. Due to its ability to influence indirect control targets, stack pointer is a key artifact in attacks. We define SPI as a property comprising of two key sub-properties - Stack Localization and Stack Conservation - and implement a LLVM-based compiler prototype codenamed SPIglass that enforces SPI. We demonstrate a low implementation overhead and incremental deployability, two of the most desirable features for practical deployment. Our performance experiments show that the overhead of our defense is low in practice. We opensource SPIglass for the benefit of the community.},
booktitle = {Proceedings of the 33rd Annual Computer Security Applications Conference},
pages = {116–127},
numpages = {12},
location = {Orlando, FL, USA},
series = {ACSAC '17}
}
```
