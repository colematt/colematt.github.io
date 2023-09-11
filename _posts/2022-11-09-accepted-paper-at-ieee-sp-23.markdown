---
layout: post
title: "Accepted Paper at IEEE S&P '23"
date:   2022-11-09 21:24:00 -0400
tags: [conferences, accepted work]
---

Our paper _Control Flow and Pointer Integrity Enforcement in a Secure Tagged Architecture_ by Ravi Theja Gollapudi, Gokturk Yuksek, David Demicco, Matthew Cole, Gaurav Kothari Rohit Kulkarni, Xin Zhang, Kanad Ghose, Aravind Prakash and Zerksis Umrigar has been accepted at [44th IEEE Symposium on Security and Privacy (IEEE S&P 2023)](https://www.ieee-security.org/TC/SP2023/).
I'm particularly proud of this work, as it's the culmination of over five years of work under the [DARPA System Security Integration Through Hardware and Firmware (SSITH) Program](https://www.darpa.mil/program/ssith) to provide secure architectures for systems that are essential to modern life.

<!--more-->

```bibtex
@INPROCEEDINGS{10179416,
  author={Gollapudi, Ravi Theja and Yuksek, Gokturk and Demicco, David and Cole, Matthew and Kothari, Gaurav and Kulkarni, Rohit and Zhang, Xin and Ghose, Kanad and Prakash, Aravind and Umrigar, Zerksis},
  booktitle={2023 IEEE Symposium on Security and Privacy (SP)}, 
  title={Control Flow and Pointer Integrity Enforcement in a Secure Tagged Architecture}, 
  year={2023},
  volume={},
  number={},
  pages={2974-2989},
  abstract={Control flow attacks exploit software vulnerabilities to divert the flow of control into unintended paths to ultimately execute attack code. This paper explores the use of instruction and data tagging as a general means of thwarting such control flow attacks, including attacks that rely on violating pointer integrity. Using specific types of narrow-width data tags along with narrow-width instruction tags embedded within the binary facilitates the security policies required to protect against such attacks, leading to a practically viable solution. Co-locating instruction tags close to their corresponding instructions within cache lines eliminates the need for separate mechanisms for instruction tag accesses. Information gleaned from the analysis phase of a compiler is augmented and used to generate the instruction and data tags. A full-stack implementation that consists of a modified LLVM compiler, modified Linux OS support for tags and a FPGA-implemented CPU hardware prototype for enforcing CFI, data pointer and code pointer integrity is demonstrated. With a modest hardware enhancement, the execution time of benchmark applications on the prototype system is shown to be limited to low, single-digit percentages of a baseline system without tagging.},
  keywords={},
  doi={10.1109/SP46215.2023.10179416},
  ISSN={2375-1207},
  month={May},}
```
