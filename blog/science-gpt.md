---
title: Large language models in academic research
subtitle: 'Can such models make research more productive?'
excerpt: >-
  By asking to produce a more efficient version of the output, a new script is provided with many performance and memory optimisations.
date: '2023-08-23'
thumb_image: images/post_33_thumb.jpg
image: images/post_33.jpg
layout: post
---


# Hello!

Over the last months, there has been an astounding progress in artificial intelligence and the development of Large Language Models (LLMs) like Chat-GPT. Briefly, this technology enables a new level of interaction with computational systems where users can provide a request and the system will interpret it and produce an output according to the requirements detected. Although far from flawless and thoroughly reliable, this development period has allowed users to experience this ground-breaking technology and understand how such tools can support their work and daily life. There has also been an interest in applying these models in academic contexts, with some researchers listing them as co-authors on papers while publishers rush to define criteria for how scientists should use this technology. Indeed, many people have praised their brainstorming abilities, as well as becoming powerful assistants in academic writing or discovering new papers. I have also been exploring the capabilities and limitations of some LLMs, mainly from a computational perspective, and in this post, I would like to share some of the applications that I have found helpful.

[1. Code translation](#translate)

[2. System setup and maintenance](#maintenance)

[3. Learning new software](#learning)

# <a name="translate">Code translation</a>

In our research, we rely on software developed in different programming environments. From Python to MATLAB, or even a C/C++ toolbox from the imaging devices, our analysis may require performing steps that are only available in each codebase. For that reason, we have been putting an effort to bring as many tools as possible to our core framework in Python and C++. This task has required porting substantial amounts of scripts from one programming language to another, followed by exhaustive testing and validation to ensure an equivalent implementation. However, with the support of Chat-GPT, this task is becoming more manageable.

In my workflow, I begin by providing an example of the code in the original language and request a translation to Python. As the output is generated, it is possible to identify potential points for improvement. Indeed, I was amazed to see that, just by asking to produce a more efficient version of the output, a new script is provided with many performance and memory optimisations. This technique works particularly well for well-defined functions which can be translated and optimised individually rather than complete codebases with multiple files. Still, it makes it much simpler to generate an initial template of the script in our target language, from which we can make improvements and adjust to our needs. Given that there is some memory of the inputs provided to Chat-GPT, we can even ask questions about parts of the script to understand them in more detail or request additional examples.


# <a name="maintenance">System setup and maintenance</a>
A second application relates to system administration tasks that we also perform in our group. Despite having an IT support team for most inquiries, we also perform particular operations internally when installing or updating software on our virtual machines. Similarly, when ETH Services perform external updates on our systems, some packages no longer work or may have incompatibilities. In these situations, Chat-GPT can be very helpful in investigating the cause of the issue. Specifically, given the customisation we have implemented in our machines, it is not always clear what package is incompatible, and by providing the error traceback to Chat-GPT, we often get a clearer idea of the exact package and the type of issue. More importantly, Chat-GPT often provides the precise command line input to solve the problem.

In any case, there have also been instances that require more care when providing input to Chat-GPT. For example, when the solutions obtained need either non-existent commands or a different system version. These situations reflect the importance of being specific and extensive when using such models to maximise the chances of obtaining the best possible outcome. Indeed, more minor adjustments to the input where we include any detail about versions we are using can directly lead to a working solution. Still, I would also remark on some cases, mostly when asking questions about Git, where Chat-GPT repeatedly provided commands that were not functional and, so far, I have not been able to adjust my input to reach a successful outcome.


# <a name="learning">Learning new software</a>
At last, Chat-GPT is a precious ally when learning a new package or software. In our academic context, we may require a specific tool for a part of a larger project, and it can be daunting when we must become reasonably comfortable using it until we can generate meaningful results. In these situations, Chat-GPT can provide accessible step-by-step examples and tutorials for smaller tasks that eventually build up towards the application we are targeting. For instance, whether I was learning about a Python package or an application, I could obtain clear instructions on achieving a specific goal, often with code examples.

This support saves a considerable amount of time with the advantage of being more tailored to our target than most tutorials we would find online. Indeed, I have had projects where I had to go through a series of online tutorials, which felt overwhelming and required substantial adjustments until I could implement my version of my project.

Nonetheless, I have encountered similar challenges as above, where the commands or steps provided by Chat-GPT were not available in my software version, requiring some subsequent exchange until a working solution was achieved.


# Conclusion
I am genuinely amazed at the potential of such large language models and the positive impact they can bring to so many (academic) fields. Apart from these computational applications, we have also been exploring in the group the capabilities of Chat-GPT to support academic writing. On that note, the results have been mixed and I have not yet identified a successful approach to consistently generate productive outputs for such tasks. Given that new advancements are being shared every day, I am excited to follow the development of this technology and continue experimenting with it to understand how it can support me.

Please feel free to [share](https://twitter.com/_franciscomcm) your thoughts on these large language models!

Have a great day!
