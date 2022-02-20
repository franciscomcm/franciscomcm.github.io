---
title: Scalable computational experiments.
subtitle: 'My strategies for designing computational studies.'
excerpt: >-
  Given how easy it is for in silico experiments to become more complex 'by adding just one more analysis', these initial questions also help decide on the most relevant results and the most effective way to present them clearly in a coherent story.
date: '2022-02-20'
thumb_image: images/post_15_thumb.jpg
image: images/post_15.jpg
layout: post
---

# Hello!

I have always been fascinated by the power of computational models to support in vivo experiments. Indeed, as a doctoral student working on a computational project, most of my research work revolves around designing and carrying out experiments in the context of image analysis. Although it could seem that computational work only requires some programming, there is still a significant amount of preparation needed to perform a study. Therefore, in this post, I would like to share some of the approaches I use when designing my computational experiments to be scalable and efficient.


[1. Planning the study workflow](#workflow_notes)

[2. Prototyping modular code](#modular_code)

[3. Designing versatile classes](#master_class)

[4. Automating repetitive tasks](#repetition)


# <a name="workflow_notes">Planning the study workflow</a>

First, unsurprisingly, I begin by planning the experiment with as much detail as possible on my [lab notebook](https://franciscomcm.github.io/blog/four-tools-for-personal-productivity/#the_hub). Specifically, I find it helpful to start by listing the scientific questions I would like to answer, which often serve as the basis for individual experiments. Furthermore, these provide a clear motivation and purpose of the work, very handy at later stages when organising and reporting the results in a presentation or journal article. Specifically, given how easy it is for *in silico* experiments to become more complex “by adding just one more analysis”, these initial questions also help decide on the most relevant results and the most effective way to present them clearly in a coherent story.

> "A good system shortens the road to the goal." – Orison Swett Marden

In a second step, I incorporate technical details like the number and references of the samples to be analysed, the variables to be tested, or the workflow from raw data to the desired output. This stage helps estimate the amount of time and computational resources to complete the analysis and simplifies the implementation stage by having a clear set of paths and variables that need to be incorporated in our code to stay organised and support the overall goal. Again, as the complexity of the project increases, having detailed documentation explaining the purpose of specific variable names or structures is truly helpful.


Also, these notes are not definitive; instead, as the work evolves, they are often revisited and updated to incorporate new ideas or adjustments.


# <a name="modular_code">Prototyping modular code</a>

After drafting the experimental plan, it is time to write the first lines of code. At this point, my goal is to build all the individual pieces needed for different steps of the analysis, from data I/O, pre-processing operations, core simulations, export results, to name a few. Since our group has a dedicated JupyterLab server, I usually create Jupyter notebooks to prototype the code for each task. Depending on the complexity, these notebooks can be very helpful to create visualisations to check the outputs of intermediate stages and ensure correct implementations. Ultimately, as each portion of code becomes more structured, I organise them in functions and modules that can be imported in subsequent notebooks targeting later steps.

On a different note, although the functions from these notebooks reflect early-stage code, I find it essential to include documentation and comments for each one justifying some implementation decisions or describing the type and format of arguments needed. It is a way to connect the code to the plan made before, and it also helps to quickly retrieve this information without having to review the script every time.


# <a name="master_class">Designing versatile classes</a>

Many of the posts focused on topics that were especially pertinent to my work in that month or referred to events I had participated in. Overall, a target of one post per month was a good compromise that did not interfere with my schedule while giving me enough room to pick a topic to cover. In retrospect, I find these posts an excellent opportunity to keep a collection of exciting highlights of my doctoral studies and likely worth looking back on as I progress in my journey. Furthermore, describing specific tools or events allowed me to step back and identify the most essential details worth sharing, again, as it would be required when drafting a manuscript after finishing an experiment. Moreover, the programming-oriented posts included several commands that I used at work and keeping them organised with simple examples was an excellent resource for every time I needed a quick reminder.


# <a name="repetition">Automating repetitive tasks</a>

Finally, to run a large-scale analysis on an HPC cluster, we often need to organise individual trials in jobs, which are then submitted to a queueing system that manages the resources available and decides which jobs to run given their requirements. Therefore, an additional module to include in our package must focus specifically on job submission and, recalling the details in the experimental plan, support the creation of the directories where each analysis will run, store the corresponding job submission script and the generated output files. Indeed, for experiments with thousands of test cases, such an approach is inevitable as it would take a very long time to submit each job manually.

Furthermore, it is also essential to have a batch submission script that submits the script of each simulation, yielding a fully automated analysis. It should be noted that before submitting our complete set of tests, I find it helpful to test simulations and calibrate the resources needed; that is, checking the duration, maximum memory required, and the optimal number of cores needed such that we provide the most accurate information to the queueing system.

At the same time, after submitting thousands of jobs, it is convenient to have a set of scripts to check all the output directories for completed simulations, tracking the progress of our experiments. It can also help identify issues with some experiments that crash unexpectedly or have unforeseen resource demands, making our code more robust after being fixed.


# Conclusion

In conclusion, these are some of the techniques I apply when designing and carrying out my computational experiments. I actively try to learn better strategies to manage my data and develop my programming abilities to match the latest standards and practices, but there is still room to improve!

Please feel free to [share your thoughts](https://twitter.com/_franciscomcm) and experiences on your computational work!

Have a great day!
