---
title: Designing figure panels.
subtitle: 'Tips and tricks to standardise figures across different plots.'
excerpt: >-
  For each figure panel, I write a one-sentence summary to describe what is the main result that readers should take from it.
date: '2022-07-24'
thumb_image: images/post_20_thumb.jpg
image: images/post_20.jpg
layout: post
---


# Hello!

An essential component for effective science communication is the ability to summarise results in clear and interpretable figure panels. Previous posts have highlighted different aspects supporting this goal, from generating auxiliary animated visualisations of the concepts being presented to introducing simple techniques to improve clarity in plots. In this post, I would like to expand on the latter idea and highlight more techniques and resources that have been foundational for my workflow to produce figure panels in my daily work. Note that the following items aim to be implemented when the figure drafts are ready, and we intend to make them more consistent altogether.

# <a name="figure_settings">Standardising figure settings</a>

First, it is important to adjust the settings of the figures to the target application since plots designed for a presentation follow different style requirements than figure panels for publications. Therefore, a useful first step is to explore the ideal definitions and settle on a template of rules that can be applied in subsequent figures. Matplotlib, one of the most well-established plotting package in Python, offers the ability to customise `rcParams` easily which effectively determine the global settings for font-sizes of titles, axis labels, legends or the style of plot lines and markers. Personally, I usually define the size for all fonts and only adjust line and marker styles depending on the type of plots I need. For this purpose, Jupyter notebooks are especially handy as we can easily re-run cells with different settings and compare which settings we prefer.

```python
import matplotlib.pyplot as plt
FONT_SIZE = 8
dpi = 200

plt.rc('font', size=FONT_SIZE)          # controls default text sizes
plt.rc('axes', titlesize=FONT_SIZE)     # fontsize of the axes title
plt.rc('axes', labelsize=FONT_SIZE)     # fontsize of the x and y labels
plt.rc('xtick', labelsize=FONT_SIZE)    # fontsize of the tick labels
plt.rc('ytick', labelsize=FONT_SIZE)    # fontsize of the tick labels
plt.rc('legend', fontsize=FONT_SIZE)    # legend fontsize

plt.rc('figure', titlesize=FONT_SIZE)   # fontsize of the figure title
plt.rc('figure', dpi=dpi)               # DPI of the figure
```

On a different note, it is important to anticipate the type of plots that will be included as this also guides which colormaps to use (from divergent to sequential, for instance). In this regard, there are two resources I would like to highlight that have helped me generate colour palettes: [Colorgorical](http://vrl.cs.brown.edu/color) and [Colorbrewer](https://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3). These tools provide tremendous flexibility and propose a set of colours according to the given input that are aesthetically pleasant and, if needed, can even be colourblind- or print-friendly. All in all, a custom colormap can help emphasise relevant aspects of the results presented and create a more polished impression.

# <a name="gridspec_mpl">Leveraging grid arrangements</a>

Next, it is common for figure panels to contain several plots highlighting different aspects parameters of a given analysis. To this end, we can either export each figure individually and arrange them in post-processing software or systematise our plotting script to reduce the amount of editing required. Specifically, Matplotlib has a `gridspec` feature where users can define the arrangement of a figure and the subplots in it conveniently.

```python
fig_width = 10.5 # inches
fig_height = 6.5 # inches
fig = plt.figure(figsize=(fig_width, fig_height))
num_rows = 2
num_cols = 3
outer = gridspec.GridSpec(num_rows, num_cols)

ax = fig.add_subplot(outer[0,0])
```
In this example, we define a figure with a given dimension and create a grid with the number of columns and rows we need. Next, we progressively add subplots in the desired index location to produce the panel arrangement. Note that additional input parameters are available to enable even more flexibility for the grid.

# <a name="convenience">Automating plotting tasks</a>

Depending on the arrangement of the plots, it can be beneficial to share axis and labels across columns or rows of the grid previously defined. For instance, if only the parameter being plotted is changing but the remaining style is kept constant, it is convenient to define a plotting function that contains all the variations of plots we need for each position on the grid while conserving the overall layout. For me, this usually implies setting or removing axis labels, defining the number of ticks in each axis, the aspect ratio of the plot, titles, or text labels in the figure. I find this approach to make it much easier to adjust styles and maintain the code as the important plotting code is isolated in a single function. Ultimately, I define a plotting function for each “type” of plot I need to produce and re-use as much code as possible to achieve a consistent style throughout the figure panels.

# <a name="postprocessing">Optional post-processing edits</a>

After producing all the plots in Python, it is important to organise them in their final arrangement to assess how they fit the underlying message. Usually, I find it helpful to plan the sequence figure panels beforehand by listing what figures are needed, which also makes it easier to focus exactly on what is still missing. In my case, for each figure panel, I write a one-sentence summary to describe what is the main result that readers should take from it. Therefore, after assembling all panels, it is much easier to review if these ideas are properly communicated or if additional data is needed.

Currently, I export all panels from Python in SVG format and carry out the final assembly in Affinity Designer. Therefore, I still have flexibility to make minor adjustments (like spacing or change a specific font-size) while conveniently producing an overview of the plots. Furthermore, it also helps getting a better feeling for the sizes of each plot and where to place figure captions and legends.

As a last step, when all figure panels are ready, it is useful to ask someone else to review them and carefully observe if the meaning of each panel is properly captured.

# Conclusion

Clear figures and plots are a crucial element of scientific presentations and articles that require considerable effort to produce. I am continuously exploring more effective ways to display my data and communicate the results appropriately. Please feel free to [share](https://twitter.com/_franciscomcm) what are your techniques to design and create clear figures for your scientific work!

