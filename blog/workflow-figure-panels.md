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

On a different note, it is important to anticipate the type of plots that will be included as this also guides which colormaps to use (from divergent to sequential, for instance). In this regard, there are two resources I would like to highlight that have helped me generate colour palettes: [Colorgorica](http://vrl.cs.brown.edu/color) and [Colorbrewer](https://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3). These tools provide tremendous flexibility and propose a set of colours according to the given input that are aesthetically pleasant and, if needed, can even be colourblind- or print-friendly. All in all, a custom colormap can help emphasise relevant aspects of the results presented and create a more polished impression.

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

Clear figures and plots are a crucial element of scientific presentations and articles that require considerable effort to produce. I am continuously exploring more effective ways to display my data and communicate the results appropriately. Please feel free to [share] (https://twitter.com/_franciscomcm) what are your techniques to design and create clear figures for your scientific work!

Have a great day!






# Hello!

In a recent post, I shared some techniques for preparing [scientific presentations](https://franciscomcm.github.io/blog/preparing-presentations/), such as conferences or the institute's internal progress reports. Among them, I discussed how I enjoy adding animated visualisations to make the work more appealing to a general audience while also helping to illustrate a given complex operation of the project. To this end, we use routinely in the group is [Paraview](https://www.paraview.org), a powerful free visualisation software that enables stunning 2D and 3D visualisations and can be easily manipulated with Python scripts. Therefore, today I would like to share my experience designing and creating animations with this tool.

[1. Drafting a storyboard](#storyboard)

[2. Experimental phase](#experimenting_views)

[3. Producing the animation](#production)

[4. Exporting step](#export_setup)

# <a name="storyboard">Drafting a storyboard</a>

As a first step, we need to decide what we aim to illustrate and how it should support the remaining elements of the talk. The central concept is to determine what data should be prepared and in what formats and define a rough idea of the sequence of events to be shown. Since we often need to include several slides, this step also helps identify individual sections that can be presented at a time. Additionally, from my experience, rendering animations Paraview on a laptop can become a very intensive task; therefore, preparing separate blocks that can later be edited as a more extended sequence makes this workflow much more manageable.

# <a name="energy_manager">Experimental phase</a>

Next, I perform some visualisation trials to see if what was planned above translates to the desired animations. In other words, as we start rendering the data and implementing our ideas, we may encounter some limitations in what can be visualised or, more importantly, realise that the result is not as intelligible as we expected. This step helps refine the original plan and often pushes our creativity to make the best use of the software's capabilities to produce our idealised clip.

For example, in a recent animation I created, such trials helped me identify how the opacity of an image could be adjusted to make the underlying process clearer, as well as determine the best camera position. Indeed, a handy feature in Paraview is the ability to save camera positions, which is extremely useful to store transition points in the animation or compare alternative views conveniently. Specifically, as we can define a custom path for the camera movement, saving a set of start- and endpoints for the camera for each sequence is worthwhile.

Other factors worth assessing during this phase are the expected total duration of the animation, defining a convenient image size and the frame rate, which are intrinsically related to the purpose of the clip in the presentation.

Finally, a crucial step during such experiments is to save the state of Paraview (there is an option available for this in the menu) for each draft created. As the name implies, this feature stores all the information related to the data being visualised, the operations performed and camera positions, making it extremely simple to recreate a given clip. Since the final animation will ideally be built upon the most promising ideas, these files are treasured to expedite this task. Another advantage of these State files is that they allow changing the input data (as long as the new file matches the format/datasets of the original file) when opening them, which gives great flexibility to still adjust the raw data after defining several processing operations.

# <a name="production">Producing the animation</a>

Having converged on a feasible plan and prepared all the necessary data, we may begin the production phase. Usually, I start by selecting the saved states I liked the most and importing the required data. At this point, the outstanding tasks are adding image-enhancing operations and ensuring that our camera and object movements still follow our intended trajectories.

Regarding the former, Paraview has a handy tool to smooth surfaces which helps turn voxel-based images, as is the case for our micro-Computed Tomography images, into a clean structure (note: applying the smoothing filter requires calling the "Extract Surface" tool first). Depending on the image, we can adjust the number of smoothing iterations and related parameters, influencing the result and the time needed to apply it. For instance, I often pick a value between 800-1000, which takes a few seconds to run; this detail is relevant as this operation must be performed for each frame of the exported animation, directly affecting the total export time.

Concerning the camera movements, it has happened that after making some adjustments to the data, portions of the image would be momentarily out-of-scene, requiring an additional revision of the camera positions to fix it.

# <a name="export_setup">Exporting step</a>

At this point, we should have produced a state file for each clip segment that renders all the data to its final format. However, before exporting all frames, there is an additional feature in Paraview worth activating for enhanced quality: the Raycaster. This tool requires high computational resources (which is why I only activate it at the end) but produces very clean renderings for each frame; it also contains several parameters determining the number of rays to cast per pixel and the illumination scale. Finally, I should add that if there are overlapping objects of changing opacity during the animation, this feature can produce erroneous results.

Usually, I export the first round of trials for all states without a Raycaster and a lower framerate to get a feeling for the complete sequence. After reviewing all steps, I activate the Raycaster, set the desired number of frames (usually 60FPS), and let the computer export each frame to a folder. Also, I usually set the exported image size to twice the canvas size for improved quality after resizing operations.

The final step is to use any GIF maker or QuickTime Player to open the image sequence and convert the frames to a movie clip.

As an additional note, Paraview states and image-processing operations can also be performed with the corresponding Python module, which enables rendering images on High-Performance Computing platforms, if available, and conveniently allows scaling the exporting step to multiple samples in parallel, if necessary. I haven't yet explored such possibilities extensively, which is why I have left them out of this post.

# Conclusion

Animations can be a valuable asset to include in a presentation, and this is a summary of the workflow I use to produce some of my favourite clips for my talks. Please feel free to [share ](https://twitter.com/_franciscomcm) what are your techniques to design and create appealing content for scientific presentations!

Have a great day!
