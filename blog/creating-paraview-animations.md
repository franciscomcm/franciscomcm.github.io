---
title: A workflow to design Paraview animations.
subtitle: 'Wow, looks fancy!'
excerpt: >-
  "Paraview, a powerful free visualisation software to produce stunning 2D and 3D visualisations."
date: '2022-06-19'
thumb_image: images/post_19_thumb.jpg
image: images/post_19.jpg
layout: post
---

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
