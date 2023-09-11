---
layout: post
title:  "Source Code Analysis for Design Patterns"
date:   2018-05-27 00:00:00 -0000
tags: [design patterns, analysis]
---

Design pattern extraction tools analyze source code and attempt to match the code to a collection of specimen design patterns. We reviewed tools announced by peer-reviewed literature, and found that the existing tools are unsatisfactory for use by modern C++ developers and analysts.

<!--more-->

# Summary

We explored the corpus of existing design pattern extraction tools. We found papers for 9 tools. Additionally, we found citations for three other tools within the corpus, but the links to these tools were broken.

  - 6/9 supported C++. 1/9 claimed to be at least nominally language agnostic because its annotation/markup scheme can be applied to any text file.
  - 2/9 claimed open source status.
  - 6/9 were _design pattern miners_, that is, given source code they claim to be able to identify design patterns within the source code. The others were _design pattern discoverers_, that is, given annotated source code, they identify intra-class relationships that suggest that they may form a design pattern (but they cannot observe code and say “this class matches the `singleton` pattern” or “that method implements `singleton::getInstance()`”.
  - 0/9 were all of open source, available for download, support C++, and are design pattern miners.

We’ll continue to look for design pattern miners that meet our needs. Without design pattern extraction capabilities, our solution will require manual annotation and this will not scale. **We believe that design pattern discovery remains an open problem, and is profitable for reverse engineering.**

# Reviewed Works

| Tool or Paper | Languages | Open Source? | Pattern Discovery or Mining? | Notes |
|---------------|-----------|--------------|------------------------------|------|
| [DP-Miner](http://ieeexplore.ieee.org/abstract/document/4148953/?reload=true) | Java | No | Discovery | Needs a pre-constructed XMI file for project. Authors claim XMI can be generated with tools like Rational Rose. |
| [DeMIMA](http://ieeexplore.ieee.org/abstract/document/4148953/?reload=true) | C++, Java | No | Discovery | Requires documenting components with OMT class diagrams |
| [SPQR](https://www.cs.unc.edu/~smithja/SPQR.html) | ? | No (patent pending) | Mining | Introduces concept of *Elemental Design Patterns*: 26 patterns authors found simple enough to express in logical systems. Only works on these Elemental Design Patterns. |
| [Design Pattern Detection Using Similarity Scoring](http://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=4015512) | Java | No. Authors don't claim open-source status, and could not find source. | Mining | Uses similarity scoring on graph of class inheritance using Java byte code. Does not appear to be able to identify class method:pattern function mapping. |
| [DPET](https://pdfs.semanticscholar.org/27b0/1043ebdf1acc3a34a69380708b7814d9546f.pdf)| C++ | Authors do not claim open-source status, and could not find source. | Mining | - |
| [An efficient tool for recovering Design Patterns from C++ Code](http://www.jot.fm/issues/issue_2006_01/article6.pdf) | C++ | Uses proprietary software ("Understand for C++") to generate a SQL database, which their solution then analyzes. Did not provide analysis artifact reference. | Mining | Introduces ability to infer aggregations. |
| [Mining Design Patterns from C++ Source Code](https://www.inf.u-szeged.hu/~ferenc/research/balanyizs_designpatterns.pdf) (_Columbus_, _DPML_) | C++ | Authors do not claim open-source status, and could not find source. | Mining and Discovery | Introduces DPML, extending existing DP annotation schemes to mark "inheritance, composition, aggregation and association,... call delegation, object creation and operation overriding". One of first to look at function bodies, not just class' structure. |
| [Evaluating C++ Design Pattern Miner Tools](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.133.922&rep=rep1&type=pdf) (_Columbus_/_CAN_) | C++ | Yes. | Mining and Discovery | Extends/Improves Columbus. Announces availability through FrontEndArt. [Download link](http://www.frontendart.com/download.html) is dead. |
| [A Toolchain for Reverse Engineering C++ Applications](https://people.cs.clemson.edu/~malloy/publications/papers/est07/paper.pdf) (_G4RE_/_G4API_) | C++ | Yes | Neither | Paper only claims ability to perform reverse engineering analysis that may reveal design patterns.|

# Dead Ends

The following were cited as possible Design Pattern mining solutions, but links are dead:

- FUJABA : [http://www.cs.uni-paderborn.de/cs/fujaba/](http://www.cs.uni-paderborn.de/cs/fujaba/)
- PTIDEJ: [http://ptidej.iro.umontreal.ca](http://ptidej.iro.umontreal.ca/)
- CPPX: [http://swag.uwaterloo.ca/~cppx/download.html](http://swag.uwaterloo.ca/~cppx/download.html)
