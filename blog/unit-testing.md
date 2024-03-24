---
title: The importance of unit testing in Python software development
subtitle: 'Improving reliability, efficiency, and maintainability of research code.'
excerpt: >-
  Developing unit tests alongside code development forces an active dialogue between two complementary perspectives.
date: '2024-03-24'
thumb_image: images/post_40_thumb.jpg
image: images/post_40.jpg
layout: post
---

# Hello!

Unit testing is a software practice that follows software development by assessing code performance according to a defined standard. It often aims to ensure that a function produces the desired output or fails for specific edge cases. With the rise of larger, more complex software packages, unit testing helps to ensure code remains reliable, reproducible on different systems and error-free. In academia, many scientific journals request that code developed for publication be shared according to open-source standards. As a result, adopting software practices such as version control, automated testing, and continuous integration has become more prevalent in research. In this context, it is imperative to understand the importance of unit testing in software development and its potential impact on research practices. In my research work, I am also preparing a Python package and have recently started incorporating unit testing into my development. In this post, I would like to share my thoughts and experience about designing unit tests for the software I am developing.


[1. Unit-testing frameworks in Python](#testing_tools)

[2. Implementation of unit testing during Python software development](#implementation_testing)

[3. Benefits of unit-testing in Python software development](#test_benefits)


# <a name="testing_tools">Unit-testing frameworks in Python</a>

In our group, most of our software is developed in Python; hence, I will focus on the tools available in this programming language. Indeed, several frameworks have been developed for unit testing, and after some online search alongside fruitful discussions with some LLMs, I have selected `pytest` for my package. In my opinion, this package provided a simple and intuitive structure for writing and running tests. Furthermore, the report produced was straightforward and customisable (e.g., it was simple to add additional information regarding which lines in each file were not covered by the tests).

Previous colleagues who set up the groundwork for our lab's Python development environment had included some unit test-based infrastructure in the pipelines. This package is part of the Python standard library and provides a class-based approach to unit testing. Eventually, some tests were also integrated with `nose`, another package available in Python with helpful customisation options for our existing needs.

Nonetheless, a common trait of these frameworks is to provide a consistent and standardised approach to writing tests, making it easier for developers to understand and maintain the test suite. Furthermore, as we are currently using GitLab and have already established pipelines to run such tests, we can easily set up new pipelines for additional packages under development. Crucially, even while developing locally on my laptop, I can conveniently develop tests and run them to ensure they function as expected before adding them to the test collection of the complete pipeline.



# <a name="implementation_testing">Implementation of unit testing during Python software development</a>

From a practical standpoint, unit tests aim to evaluate small portions of the codebase. Essentially, one test would focus on each "unit" of the code, designed for a particular purpose. As hinted before, the goal is to ensure that when an input meets the expected conditions, it produces the desired output (in fact, comparing the function's output and the expected result is a crucial step of such unit-testing frameworks).

Furthermore, writing unit tests also helps to plan and develop code in small, focused functions designed for a single task. Comparably, it also helps to identify parts of a larger function that could be individualised to facilitate testing and code compartmentalisation. Eventually, maintaining a high level of modularity in the codebase makes it easier to maintain, understand, and expand with newer methods.

In addition, a key advantage of unit testing is that it helps identify (unforeseen) edge cases. Indeed, I have already found ways to improve the robustness of some functions against incorrect input arguments, leading to an overall more reliable and versatile implementation. At the same time, the same exercise helps identify bugs in the code that may not have been noticed so far since the function had not been tested against other cases and inputs. In other words, developing unit tests alongside code development forces an active dialogue between two complementary perspectives, one aiming at fulfilling one purpose most efficiently and cleanly possible (the primary goal of the function) and another aiming at understanding what alternative ways to reach this goal can go wrong.


# <a name="test_benefits">Benefits of unit-testing in Python software development</a>

At last, I would like to recap the main advantages of unit testing during software development. First, scientific work published with adequate unit tests provides a strong reliability stamp on the results proposed. Furthermore, being open source, the scientific community can further inspect the code and build new advancements based on this groundwork. Again, the fact that unit tests cover the original codebase allows developers to make changes, knowing they can quickly identify and address any regressions confidently.

Next, unit tests ensure that software works as expected by clearly indicating what type of input should be provided and what the expected behaviour of individual components is. This effort helps ensure the software continues functioning as expected, even as new features are added or existing ones are modified.
Additionally, it sets a standard for software code quality. With the rise of LLMs for code development, it is more straightforward to produce drafts of scripts that can be further adapted to a particular goal. By incorporating unit tests from this stage, developers can immediately identify and fix issues and have a thoughtful design process for the software.

# Conclusion

Overall, the benefits of unit testing in software development make this task an essential practice for anyone looking to build robust, reliable, and high-quality applications. By investing in a comprehensive unit testing collection, developers can reduce the risk of bugs, improve the overall quality of their codebase, and deliver software that meets the needs of their users. In academia, where such software often becomes the basis for novel, exciting scientific findings, building trust in the tools used to uncover these new insights can only be beneficial for advancing scientific knowledge further.

Please feel free to [share](https://twitter.com/_franciscomcm) your thoughts about unit testing during software development!

Have a great day!


### Acknowledgements

As an experiment, parts of this text were designed with the support of Claude-3 Haiku and Grammarly-AI based on provided notes. The image was generated with Playground.