---
layout: post
title: "Accepted Paper at NordSec '22"
date:   2022-10-06 12:42:00 -0500
tags: [conferences, accepted work]
---

Our paper _Simplex: Repurposing Intel Memory Protection Extensions for Secure Storage_ by Matthew Cole and Aravind Prakash has been accepted at [Nordic Conference on Secure IT Systems (NordSec '22)](https://nordsec2022.ru.is/#accepted-papers).
The acceptance rate was 22.5%.

<!--more-->

```bibtex
@InProceedings{10.1007/978-3-031-22295-5_12,
author="Cole, Matthew
and Prakash, Aravind",
editor="Reiser, Hans P.
and Kyas, Marcel",
title="Simplex: Repurposing Intel Memory Protection Extensions for Secure Storage",
booktitle="Secure IT Systems",
year="2022",
publisher="Springer International Publishing",
address="Cham",
pages="215--233",
abstract="The last few decades have seen several hardware-level features to enhance security, but due to security, performance, and/or usability issues these features have attracted steady criticism. One such feature is the Intel Memory Protection Extensions (MPX), an instruction set architecture extension promising spatial memory safety at a lower performance cost due to hardware-accelerated bounds checking. However, recent investigations into MPX have found that is neither as performant, accurate, nor precise as software-based spatial memory safety. Given its ubiquity, we argue that it provides an under-utilized hardware resource that can be salvaged for security purposes. We propose Simplex, an open-sourced library that re-purposes MPX registers as general purpose registers. Using Simplex, we demonstrate securely storing sensitive information directly on the hardware (e.g. encryption keys). We evaluate for performance, and find that deployment is feasible in all but the most performance-intensive code, with amortized performance overhead as low as about 1{\%}.",
isbn="978-3-031-22295-5"
}
```