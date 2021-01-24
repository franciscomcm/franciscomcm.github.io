---
title: Five useful operations with Pandas DataFrames
subtitle: 'Data science made easy!'
excerpt: >-
  Handy tricks to explore and prepare a dataset before carrying a data analysis!
date: '2021-01-24'
thumb_image: images/post_2_thumb.jpg
image: images/post_2.jpg
layout: post
---

# Hello!

This post will highlight five operations with `pandas DataFrames` that may come very handy while exploring and preparing a dataset before carrying a data analysis:

[1. Renaming columns with `.rename()`](#rename_columns)

[2. Merging DataFrames with `.concat()`](#merge_dataframes)

[3. Grouping data based on a given column with `.groupby()`](#groupby_data)

[4. Creating new columns based on existing columns with `.apply()`](#new_columns)

[5. Sub-selecting DataFrame rows based on binary masks](#masking_df)

# What is pandas?

Pandas is a Python package that provides a comprehensive set of tools to deal with tabular data. For more details on this package's development, feel free to check the [pandas website](https://pandas.pydata.org/about/).

> I see it as Microsoft Excel in Python.

I see it as Microsoft Excel in Python and, as I learn new tricks and best practices, it has become my go-to software for any data analysis I do in my work. Hence, I will now go through five operations that I find especially useful for cleaning and organising data.

```python
import numpy as np
import pandas as pd
```

# <a name="rename_columns">1. Renaming columns with `.rename()`</a>

Imagine having a set of CSV files from two thermometers measuring the temperature inside the lab throughout the day. After importing both files as pandas DataFrames, thermometer A has two columns, named `time` and `temperature_Celsius`, while thermometer B also has two columns but entitled `time` and `temp_in_Cels`. In the code-cell below, we are creating the DataFrames with different column names

Since we know both `temperature_Celsius` and `temp_in_Cels` represent the same quantity (temperature in degrees Celsius), it would be very convenient to rename them similarly.

This can be achieved with the `rename()` DataFrame function. We only have to pass a dictionary with the key-value of the change we want to do, where **keys** represent **current names** and the **values** are the **updated descriptions**.

```python
thermometer_A = pd.read_csv('../input/pandas-example/thermometer_A.csv')
thermometer_B = pd.read_csv('../input/pandas-example/thermometer_B.csv')
print('Columns of A: ', list(thermometer_A.columns))
print('Columns of B: ', list(thermometer_B.columns))

rename_A = {'temperature_Celsius': 'Temperature (ºC)'}
thermometer_A = thermometer_A.rename(columns=rename_A)
rename_B = {'temp_in_Cels': 'Temperature (ºC)'}
thermometer_B = thermometer_B.rename(columns=rename_B)

print()
print('Updated columns of A: ', list(thermometer_A.columns))
print('Updated columns of B: ', list(thermometer_B.columns))
```

In the example above, we renamed the columns of the DataFrames, but the same function can be used to rename the index of the DataFrame (passing the dictionary to `index=` instead of `columns=` in the function call).

# <a name="merge_dataframes">2. Merging DataFrames with `.concat()`</a>

Having renamed our column names, we now want to combine the DataFrames in one, containing all data from both thermometers. This is especially useful if we need to create categorical plots that highlight differences between devices.

First, we should create new columns on each DataFrame that uniquely describe the device. In this simple example, a column `Equipment` should suffice, where we fill all rows (representing different time-points) with the value `A` and `B`, respectively, for each equipment. This way, when we merge both datasets, we can still identify from which device the data came from.

Then, we can create our main DataFrame `temperature_measures`, with properly initialised columns.

```python
thermometer_A['Equipment'] = 'A'
thermometer_B['Equipment'] = 'B'

temperature_measures = pd.concat([thermometer_A, thermometer_B], axis=0, ignore_index=True)
```

Here, we pass `axis=0` so that the DataFrames are combined vertically, in long-form, and `ignore_index=True` because, in this example, the row number is not meaningful and can be reset after concatenating the data.

Other pandas functions could also serve the same purpose (ex: `append()`). Depending on your problem, they may be more suitable.

# <a name="groupby_data">3. Grouping data based on a given column with `.groupby()`</a>

Let's assume we just want to get an average of the temperature measurements, regardless of the equipment. We can use the `.groupby()` function and pass the column's name that should be used to group the data. Then, we can call further functions depending on the information we aim to compute such as `.mean()`, `.std()` (standard deviation).

```python
print(temperature_measures.groupby('Time (h)').mean())
print(temperature_measures.groupby('Time (h)').std())
```

# <a name="new_columns">4. Creating new columns based on existing columns with `.apply()`</a>

Let's consider another example where we measure the growth rate of groups of plants over four weeks, comparing two groups given new fertilisers and a control group that only received water.

The dataset contains two columns `Baseline` and `Follow-up` representing the start and endpoint for the corresponding measurement. It could be useful for plotting purposes to have a descriptor that directly indicates the interval between measurements rather than just the start or end time-point.

Therefore, we can use the `.apply()` function to create a `lambda` function that operates on the provided columns.

```python
plants_data = pd.read_csv('../input/pandas-example/fertiliser_plant_growth.csv')
print('Columns: ', list(plants_data.columns))
plants_data['Time-points'] = plants_data[['Baseline', 'Follow-up']].apply(lambda x: '-'.join(x.map(str)), axis=1)
print(plants_data)
```

For each row in the DataFrame (as we set `axis=1`), we take the values of the columns `Baseline` and `Follow-up`, convert them to `string` and join them with the marker `-`. Again, this function offers a lot more flexibility that can be tuned to your specific use-case.

# <a name="masking_df">5. Sub-selecting DataFrame rows based on binary masks</a>

Finally, another useful technique is to mask a DataFrame based on the values of the columns. Let's assume we want to compute some parameters for each group of plants.

We can create a mask based on the `Group` column's values and identify the corresponding rows of the complete DataFrame. Then, we simply pass the mask in `[]` on the DataFrame, and the correct rows will be indexed.

```python
mask_control = plants_data['Group'] == 'Control'
print(plants_data[mask_control])
```

This operation also supports multiple masks simultaneously by chaining them with `&` inside the `[]`.

```python
mask_second_follow_up = (plants_data['Follow-up'] == 2)
print(plants_data[mask_second_follow_up])
print(plants_data[mask_second_follow_up & mask_control])
```

If you prefer writing the masks directly inside the `[]` instead of creating a mask variable, make sure to wrap each one around `()` to avoid errors in the logical operations.

# Conclusion

`pandas` is a powerful package that can massively improve your workflows. Furthermore, it can be seamlessly integrated with other packages to create publication-ready figure panels (more on that later) with little effort.

If you would like to learn more about using pandas, I highly recommend [Chapter 3](https://jakevdp.github.io/PythonDataScienceHandbook/03.00-introduction-to-pandas.html) of the [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/) by Jake VanderPlas. The book covers all the basics with clear explanations and introduces some advanced techniques to best leverage this package in your work.

The data and examples shown in this post are available on [Kaggle](https://www.kaggle.com/franciscomcm/five-useful-operations-with-pandas-dataframes), where the outputs of each code cell are also shown.

Happy coding!


### Acknowledgments

Image by <a href="https://unsplash.com/@itookthose?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Sid Balachandran</a> on <a href="https://unsplash.com/s/photos/pandas?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>
