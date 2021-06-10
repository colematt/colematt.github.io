---
layout: post
title:  "Reviewing Academic Literature"
date:   2019-04-15 18:00:00 -0000
categories: [literature review]
---

% Specify reviewed paper's title and citekey
\subsection{Reviewed Paper Title}
\bibentry{citekey}


# Literature Review
## Summary
This is a one to two paragraph discussion of the paper. 
Here, summarize main points forming the structure of the paper. 
Include critical definitions introduced by the authors. 

Possible discussion points (its not necessary to address all of these):
- What is the problem? 
- How do the authors solve the problem?
- What are the authors' claimed contributions?
- How do the authors evaluate their solution?
- How do the authors position their work relative to related work?
- How is this work relevant to our work?

Avoid repeating the abstract or directly quoting large sections of the paper and do _not_ express your opinions here. 

## Analysis

This is a one paragraph analysis of the paper. To the maximum extent possible, try to use factual observations and not personal opinions. 

Possible discussion points:
- Did the authors introduce a previously unknown technique or perspective? 
- Are their findings repeatable? 
- What artifacts/tools do they make available? Did these artifacts/tools work as promised and how much effort was required? 
- Does the evaluation justify the claims? Could they have designed better evaluation? 
- Where did the authors leave loose ends? 
- Did they make an assertion or promise that they didn't validate later? 
- Are there technical errors, logical fallacies or poor assumptions within the paper? 
- Are there topics poorly explained that can't be assumed to be within a knowledgeable reader's base of knowledge?

# Rhetorical Precis

1. In a single coherent sentence give a rhetorically accurate verb (such as "assert", "argue", "deny", "refute", "prove", "disprove", "explain", etc.) and a "that" clause containing the major claim (thesis statement) of the work.
2. In a single coherent sentence give an explanation of how the author develops and supports the major claim (thesis statement).
3. In a single coherent sentence give a statement of the author’s purpose.
4. In a single coherent sentence give a description of the intended audience and/or the relationship the author establishes with the audience.

# Peer Review

At some point or the other, every researcher faces a situation where they are required to review or assess a piece of work that is loosely related or unrelated to their field of expertise. In some cases, there may be complex math involved. While math is useful and often required to succinctly convey certain concepts, unfortunately, complex math also provides a facade for weak papers to hide behind. Here are some pointers on how to review such papers:
1) Logical soundness: See if the paper makes logical sense. This is a big picture assessment where you look at the introduction, methods and evaluation to see if they all add up with a flow of logical reasoning. Here, you are not looking to understand the details of the paper, rather you focus on the high level idea.
2) Problem relevance: See if the paper is relevant to the conference and whether the problem the paper is trying to solve is a real problem. Some papers create problems to solve, and we want to flag them. Relevance should be clear in the first 2 sections of the paper. If you are not familiar with the topic, you may have to read 1-2 well cited papers to get some context.
3) Satisfactory evaluation: Does the evaluation sufficiently substantiate the claims? Are there any outlying results? If so, is there a justification and/or supporting theories for outlying results? If you did not understand the body of the paper, assume it to be correct and examine the evaluation with respect to the claims in the introduction.
4) Understanding equations: While some equations may be intuitive and easy to understand, not all equations are straightforward. One strategy that usually fishes out fake or meaningless equations without a necessity to actually understand them is the check for dimensional correctness. The dimensions (or type) of left hand side of an equation should be equal to the dimensions of the right hand side.
5) Plagiarism or repeat submissions: A simple google search for some key words (not necessarily the title) should tell whether the paper has previously appeared.
6) Writing quality: Grammar issues are easy to flag, and a significant number of them is an automatic reject.

In spite of all the above, it may still be hard to review some papers. In such cases, we present our understanding (whatever that is) along with an assessment of the above points and recommend an accept. As a rule of thumb, we never reject papers that we are not familiar with. We accept or weak accept and request the PC chair for additional reviews. Statistically, a paper that makes zero sense to an active researcher—even with different expertise—has a very low probability of acceptance. In other words, every accepted paper should make at least some high-level sense to every security researcher.
