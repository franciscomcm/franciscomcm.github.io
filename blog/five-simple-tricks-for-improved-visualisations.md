---
title: Five simple tricks for improved visualisations
subtitle: 'Towards clearer figures with Matplotlib and Seaborn!'
excerpt: >-
  Easy tricks to improve the readability of visualisations!
date: '2021-03-21'
thumb_image: images/post_4_thumb.jpg
image: images/post_4.jpg
layout: post
---

# Hello!

In this post, I would like to focus on the challenge of creating clear scientific figures and how they can help readers better understand our results. Communication is an intrinsic element of our lives, and our ability to convey our message is crucial to achieving fruitful connections with others. Science is no exception, and displaying our findings clearly is an essential step of any scientific project, helping our audience understand the relevance of our (complicated) work.

In a [previous notebook](https://www.kaggle.com/franciscomcm/five-useful-operations-with-pandas-dataframes), Pandas DataFrames were presented as a helpful tool to organise data and run typical data exploratory analysis. Here, we will focus on five simple tricks that I believe can significantly improve the overall quality of the figures created with [Matplotlib](https://matplotlib.org)/[Seaborn](https://seaborn.pydata.org/index.html):


[1. Adjust the font size of the labels](#font_sizes)

[2. Select a colormap](#select_colormap)

[3. Adjust the step of axis ticks](#axis_ticks)

[4. Have a descriptive legend](#full_legend)

[5. Use Latex symbols in labels](#latex_ftw)


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

# <a name="font_sizes">1. Adjust the font size of the labels</a>

In my opinion, the default font size of Matplotlib is too small for clear readability, especially when the figures are shown in presentations. Therefore, one of the first settings I adjust when I start creating visualisations is the font size, which can be done at a general level or by individually adjusting each label.

I prefer to set the global scale in Python and later make minor adjustments in post-processing (ex: in Figma) if needed. Both Matplotlib and Seaborn have options to change these details with different degrees of complexity, but for an easy-to-remember command, we can simply do `sns.set(font_scale=1.5)`.

Seaborn also has a command to select the "context" of the figure, which automatically sets pre-defined recommendations depending on the purpose of the figure:

`sns.set_context(‘paper’)`, where the remaining options are `'poster'`, `'talk'`, `'notebook'`. Here, we could also include the `font_scale` argument. These are good starting points, which can then be manually tuned to your preferences with little effort.


```python
x_values = np.arange(5)
y_values = np.random.randn(5)

sns.set(font_scale=1)
plt.figure()
plt.plot(x_values, y_values)
plt.title('Default font size')
plt.xlabel('X variable')
plt.ylabel('Y variable')

sns.set(font_scale=1.3) # Values between 1.3 and 2 generally work well
plt.figure()
plt.title('Scaled font size')
plt.plot(x_values, y_values)
plt.xlabel('X variable')
plt.ylabel('Y variable')
plt.show()
```


# <a name="select_colormap">2. Select a colormap</a>

Given that digital access to scientific publications is becoming increasingly more established, figures can now benefit from a broader combination of colours, symbols, line styles and widths that are not restricted by their interpretability in a grayscale printed paper, perhaps regarded as a limiting factor in the past. In any case, it is vital to select a set of colours that helps to interpret the figure (and which may not always be the case when using default settings).

There are many guidelines on selecting an appropriate colormap depending on the type of figure. Still, for now, we will focus on the commands used to define the colors for some of the most common plotting functions:

- Functions like `plot`, `scatter`, `fill_between` from Matplotlib (which plot one set of data per call): typically, there is an argument `color` that can be followed by a string with the color name. At each function call, the user can specify the color to be used; otherwise, the colors will be picked sequentially from the active colormap. A detailed list of the available color options is given [here](https://matplotlib.org/stable/gallery/color/named_colors.html).
- Functions representing 2D or 3D data or surfaces, like `imshow`, `hist2d` from Matplotlib: the argument `cmap` allows setting the colormap to use in the figure. Detailed documentation of the available colormaps is given [here](https://matplotlib.org/stable/tutorials/colors/colormaps.html).
- Functions from [Seaborn](https://seaborn.pydata.org/tutorial.html): the argument `palette` allows passing a string with the name of the colormap to be used. Like the link given above, Seaborn also has a detailed [documentation page](https://seaborn.pydata.org/tutorial/color_palettes.html?highlight=palette) describing different ways to set color palettes for the figures. Furthermore, as in [1. Adjust the font size of the labels](#font_sizes), Seaborn also provides a one-line command to set the palette for the figures: `sns.color_palette("palette_name")`



```python
plt.figure()
plt.plot(x_values, y_values, color='red')       # User-defined color
plt.plot(x_values, y_values/2, color='blue')    # User-defined color
plt.plot(x_values, y_values/3)                  # Default Matplotlib colormap
plt.plot(x_values, y_values/4)                  # Default Matplotlib colormap
plt.show()

plt.figure()
plt.hist2d(x_values, y_values, cmap='viridis')  # User-defined colormap
plt.show()

sns.set_palette('Set2')
plt.figure()
sns.lineplot(x=x_values, y=y_values)
plt.show()
```


# <a name="axis_ticks">3. Adjust the step of axis ticks</a>

Matplotlib usually tries to optimise the space in the axis to display the necessary information without overloading the figure. However, there may be cases where we want to specifically include a set of ticks in our axis, for instance, to highlight the temporal evolution of the data. Therefore, we can easily set the step of the ticks we want to use and couple it with settings for the axis limits to emphasise the interval of values of our data or the range that we specifically want to highlight.

The example below is applied on the horizontal axis, but the same commands are obviously valid for the vertical axis.


```python
import matplotlib.ticker as plticker

fig, ax = plt.subplots(1,1,figsize=(5,5))  # Initialise figure
loc = plticker.MultipleLocator(base=0.5)   # Create ticker at `base` intervals
ax.plot(x_values, y_values)                # Create plot
ax.xaxis.set_major_locator(loc)            # Set ticker
ax.set_xlim([1,4])                         # Set axis limits
plt.show()
```

# <a name="full_legend">4. Have a descriptive legend</a>

Legends and figure captions are essential pieces of any visualisation, helping to characterise the symbols and colours describing the data presented. Like the font size adjustments, we can include a legend while plotting data in Python and later make any post-processing adjustments if necessary.

In this case, I would like to draw attention to a setting in Seaborn, which filters the amount of information displayed: `legend='full'` (the remaining settings are `'auto'`, `'brief'` or `False`).

I prefer setting this argument to `'full'` and include all the information from the plot in the legend.

Two additional commands that are very handy when manipulating legends are [loc](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.legend.html) and `bbox_inches='tight'` for exporting the figure and ensuring the legend is not cropped.


```python
# Prepare dummy data
group_0 = np.stack([x_values, y_values, np.repeat(0, x_values.shape)], axis=1)
group_1 = np.stack([x_values, 2*y_values, np.repeat(1, x_values.shape)], axis=1)
group_2 = np.stack([x_values, 3*y_values, np.repeat(2, x_values.shape)], axis=1)
plot_data = pd.DataFrame(data=np.concatenate([group_0, group_1, group_2], axis=0), columns=['X', 'Y', 'Group'])
print(plot_data)

plt.figure()
plot = sns.lineplot(x='X', y='Y', data=plot_data, hue='Group', legend='full') # Set legend to full and edit the location in post-processing
# Saving the figure with the `bbox_inches` option
# plt.savefig(save_path, bbox_inches='tight')
plt.show()

plt.figure()
plot = sns.lineplot(x='X', y='Y', data=plot_data, hue='Group', legend='full')
plt.legend(title='Group', loc='right') # Set legend with Matplotlib and specify the location
plt.show()
```

# <a name="latex_ftw">5. Use Latex symbols in labels</a>

Finally, I would like to emphasise the importance of adding appropriate units to all relevant plot labels, as it facilitates readability and improves the completeness of the figure. In this regard, it is common to plot data whose units are described with Greek letters or specific symbols. For these cases, we can leverage Matplotlib's ability to incorporate Latex symbols in labels and ultimately make our figures look more professional.


```python
plt.figure()
sns.lineplot(x='X', y='Y', data=plot_data, hue='Group', legend='full')
plt.ylabel(r'$\sigma$ diameter ($\mu$m)')  # Note: this is a random label with not real meaning
plt.xlabel('Time (days)')
plt.show()
```

# Conclusion

Matplotlib and Seaborn are extremely powerful Python packages to produce publication-ready figures. I thoroughly recommend investing the time to learn how to leverage their capabilities to create interpretable plots. As mentioned in a previous post, the [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/) from Jake VanderPlas has a great introduction to a wide range of commonly used Matplotlib functions as well as some advanced techniques ([Chapter 4](https://jakevdp.github.io/PythonDataScienceHandbook/04.00-introduction-to-matplotlib.html)). Regarding Seaborn, I would recommend their own documentation page, which contains succinct but diverse examples highlighting the versatility of this package for multiple applications.

Here, I presented a list of some of the tricks I commonly use when preparing visualisations. There are obviously many more valuable tips that fit the preferences of each author and case. Feel free to share some of the practices you find helpful in your workflows!

The data and examples shown in this post are available on [Kaggle](https://www.kaggle.com/franciscomcm/five-simple-tricks-for-improved-visualisations), where the outputs of each code cell are also shown.

Have a great day, and happy coding!


### Acknowledgments

Image by <a href="https://unsplash.com/@yucar?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">YUCAR FotoGrafik</a> on <a href="/s/photos/sea?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
