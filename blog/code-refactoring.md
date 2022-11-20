---
title: The art of code refactoring
subtitle: 'Can we turn good into great?'
excerpt: >-
  In my mind, refactoring code resembles the work needed to restore a car or watch.
date: '2022-09-18'
thumb_image: images/post_22_thumb.jpg
image: images/post_22.jpg
layout: post
---


# Hello!

Programming is an essential skill for my scientific work, constantly challenging me to learn new techniques and improve my capabilities. Furthermore, as with spoken languages, it enables developers to easily share code and tools others can interpret and use to create novel products. Nonetheless, this process may require refactoring existing code to our needs or achieving improved performance and reliability. In my case, it happened that I picked up projects started by previous doctoral students, which required exploring and understanding their code and adapting it to the questions we aimed to answer in newer studies. Therefore, in this post, I would like to share my workflow to review and refactor code.

[1. Code exploration](#code_explorer)

[2. Rewriting and experimentation](#experimenting)

[3. Validation and benchmarking](#validation)

# <a name="code_explorer">Code exploration</a>

In my mind, refactoring code resembles the work needed to restore a car or watch. The entire piece is disassembled into individual parts, and their state is carefully evaluated. Some may require a replacement, while others are deemed acceptable, and the components can be mounted again to restore the original shape. When starting out, a helpful first step is to collect all the scripts required and understand the flow of the analysis from start to finish. Depending on the project's magnitude, writing or drawing such a schematic can be very helpful, giving clarity on which classes and functions are most important and providing a first impression of the state of the code and which sections may require further rework.

After this initial overview, I perform a more careful review where the goal is to fully comprehend the purpose of each line. At this stage, I aim to generously add comments throughout the scripts explaining relevant details and, crucially, leave notes for potential improvements. From a practical perspective, I complement these comments with one-word flags (like: `TRY`, `TODO`, `CHECK`) that target different stages of the refactoring process and help me scan long scripts more efficiently and prioritise the work ahead.

At this point, not only should we have a solid understanding of the entire workflow, but we also identified which pieces require more attention or should be optimised, and we can proceed.


# <a name="experimenting">Rewriting and experimentation</a>

Refactoring existing code should have the final goal in mind, balancing the effort and the benefits of replacing the sections identified previously. Specifically, some projects may justify rewriting an entire class to make it more user-friendly, while improving individual functions of a script may suffice for others. Based on the comments left in the first review stage, I begin by searching which ones can be solved by packages already available. Very often, someone has already faced a similar problem and may have developed a working tool that can be imported to replace more rudimentary implementations produced in the initial stages of the development of the code. Furthermore, I find it helpful to keep the workflow diagram nearby as it has happened that such packages end up simplifying steps of the analysis by providing several features simultaneously (which would otherwise be computed individually). Conversely, this step can also highlight the (undocumented) reason for certain design decisions in the pipeline and why it may have intentionally not relied on existing packages to compute a particular step.

This step can involve quite some trial and error to identify the best approach to improve a given function. My strategy is to save intermediate outputs of the analysis that act as checkpoints, helping to focus on the section at hand without having to re-run the entire workflow every time to reach the function of interest. Furthermore, I still add several comments (often with the `CHECK` flag) with ideas for further improvements if the current implementation is not good enough or if anticipated bottlenecks end up having a strong influence on the execution.

I find it helpful to carry out this step in Jupyter Notebooks, where it is effortless to try out several ideas and progressively build the final function in subsequent cells. Additionally, breaking tasks into individual steps gives a more refined perception of their performance requirements, which can benefit code optimisation stages. Also, depending on the use case and the input data size, it may help to generate a smaller, working version of the dataset that can efficiently be loaded for development purposes.

> "The real problem is that programmers have spent far too much time worrying about efficiency in the wrong places and at the wrong times; premature optimisation is the root of all evil (or at least most of it) in programming." -  Donald Knuth


# <a name="validation">Validation and benchmarking</a>

Finally, having revamped individual functions of the workflow, it is essential to ensure they still produce the same results as the original code. For instance, a pipeline may have been developed to explore a scientific question and validated, but it never got fully optimised for general use. In such cases, I try to isolate the variables or values at different checkpoints in the new workflow with an analogous element on the original pipeline and perform a stepwise comparison. From specific values, we can advance to complete functions and expand to the whole workflow; I also find it helpful to keep track of each step's execution time and memory consumption as it provides a more tangible metric to compare both versions.

It is also essential to review all comments left initially and give special attention to (`CHECK`-like) flags referring to possible issues to ensure these are not interfering with the code execution. As a final step, the entire dataset may be analysed, and the output compared with that generated independently by the original creator of the workflow.


# Conclusion

Understanding and improving code can be challenging; nonetheless, developing the skills needed to identify bottlenecks and planning more efficient solutions for each step can be extremely valuable to becoming a proficient programmer. Furthermore, I find it very rewarding to learn and implement good programming practices, which make code refactoring much more manageable and, ultimately, come up with improved scripts than those we started.

Please feel free to [share](https://twitter.com/_franciscomcm) what are your techniques to refactor code!

Have a great day!
