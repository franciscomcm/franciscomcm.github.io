---
title: Dealing with challenges
subtitle: 'Science is unpredictable.'
excerpt: >-
  Some details of such methods may lead to an insight when dealing with my own data.
date: '2024-08-31'
thumb_image: images/post_45_thumb.jpg
image: images/post_45.jpg
layout: post
---


# Hello!

Science is unpredictable, and one of the most exciting aspects of research is the ability to think about a process, propose a hypothesis that could explain it and collect data to test it. Crucially, there is more to research than collecting data from our experiment. An equally pivotal step is the analysis of such datasets to derive meaningful conclusions. However, depending on the complexity of the problem, defining a clear analysis pipeline that produces interpretable results can be a challenge on its own. Recently, I have been dealing with this situation, where I am learning how to process my data to test the hypothesis we originally devised. Hence, in this post, I would like to share my experience and learnings while conducting my research.


[1. Building a solid technical basis](#technical_basis)

[2. Fast to iterate](#iterations)

[3. Interactive discussions](#discussions)


# <a name="technical_basis">Building a solid technical basis</a>

Throughout my doctoral research, I have always tried to be comfortable with the fundamental techniques used in typical data analysis pipelines. Additionally, as I encounter new articles and papers that feature methods similar to those I am exploring, I aim to learn and understand the concepts used for the analysis presented. Often, these may not be directly related to my work, but as a firm believer in knowledge cross-pollination, some details of such methods may lead to an insight when dealing with my own data. Additionally, I aim to refresh my knowledge of other well-established techniques (many of which were initially introduced to me during lectures) and iteratively review their details as needed. In this regard, a prominent yet often disregarded aspect to consider is the domain of applicability of a given method (i.e., under which conditions can it be applied) and for what purpose (i.e., is it a diagnostic tool to run before another approach or an evaluation measurement of the outcome). The work in some articles has happened to bend these conditions favourably to the results presented, which may lead to decreased confidence in the analysis shown. Hence, knowing and respecting these limits can help improve the robustness of our approach and conclusions derived from it.

Since my work is computationally oriented, and I code primarily with Python, I also leverage the robust codebase available for this language. Data-analysis-oriented packages such as scipy, numpy, scikit-learn or statsmodels have incredible documentation pages that provide detailed descriptions of the methods implemented and include references to scientific articles where these were introduced. Often, studying such documentation pages is a valuable first step to acquiring knowledge on techniques that may be useful in our work and enables us to identify the most promising ones. Besides, given the excellent structure of such packages, it is relatively simple to try out different models on synthetic or real data and evaluate the performance.


# <a name="iterations">Fast to iterate</a>

Indeed, the ability to try many methods quickly has been another critical aspect worth noting. When starting, it may need to be clarified which method is most suitable to process our data; for example, for a simple sample clustering, scikit-learn provides several methods that excel at different tasks. However, given that they share the base constructor in the implementation, it is straightforward to swap them until the most successful approach for our data is identified. However, data processing is often more complex and in such cases, it is worth spending some extra time creating custom scripts that enable any user to try out combinations of parameters in a systematic way. From there, results can be generated in a structured fashion and easily compared.

On this note, another crucial element to consider when producing data, especially in computational work, is always considering which measures can be used to evaluate the performance of the methods we apply. Different domains inevitably have specific targets, but the key message is to verify, at every stage, that the data and processing steps we apply are accurate or conserve the accuracy and precision from previous steps. While this may look cumbersome work, it is the type of results that could be presented in the supporting materials on a paper and strongly improve the confidence in the work, as we provide openly the metrics that describe the performance of our analysis.


# <a name="discussions">Interactive discussions</a>

Finally, as research is aimed to be shared with the scientific community, it is essential to present and discuss our results with others. The most accurate and reproducible approach may fall short if no one else can interpret the results it produces. Hence, building on the previous point, I iteratively try to incorporate an external viewpoint into the analysis to get an "independent" perspective. The most straightforward approach is to share an overview of our approach (without necessarily revealing critical aspects of our experiment or data) with AI assistants and discuss in a chat how they perceive it. Since it is readily available, we can inquire about what is already good and what could be improved and even collect ideas for additional analysis that could be worth exploring. Not only that, as most of these assistants can also work with code, we can discuss whether our implementation is correct and request improvements in performance or usability.

Additionally, towards a more realistic proxy of the scientific community, scheduling meetings with my supervisor (or any experienced researcher in the field) provides a much clearer idea of how the work would be perceived. Besides, as the supervisor is also the leader driving the research direction, such meetings are beneficial for brainstorming ideas of what else could be worth exploring that is aligned with how they would like the project to evolve. As hinted previously, supervisors often have very creative ideas of what they would like to see, and I find it quite exciting to converge on an approach that meets those aspirations while remaining technically sound from a methodological perspective.


# Conclusion

Dealing with my current dataset has been an eye-opening challenge, and I am really excited to finalise this part of the work. While there are still open questions to solve in my implementation, the approaches described above will continue to help me progress and reach a fruitful outcome.

Please feel free to [share your thoughts](https://twitter.com/_franciscomcm) about tackling challenging scientific questions!

Have a great day!
