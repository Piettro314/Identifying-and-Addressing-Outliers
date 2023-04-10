<h1 align="center" style="color:MediumSeaGreen;"> <b> Technique To Identify & Address Outliers </b></h1>

# Preface

When developing a regression model, outliers can distort the predictions as the model endeavors to achieve the best possible fit to the provided data. Therefore, it is crucial not only to identify the outliers for improved predictions but also for analysis, as they can sometimes reveal patterns that are not otherwise evident as part of the entire dataset.

# Overview

This short project is a walkthrough of how outliers are identified and set aside for further analysis.

# Data

Airbnb [European cities](https://zenodo.org/record/4446043#.Y9Y9ENJBwUE)


# Exploratory Data Analysis 
Using the ydata_profiling Python library, it is possible to detect outliers in a dataset. This library provides a concise code that enables a rapid assessment of the entire dataset, enabling further analysis. In this particular demonstration, the focus is on the <b>Alerts</b> tab, which reveals a significant deviation in the cost per night for CAD.

```
profile = ProfileReport(data)
profile.to_notebook_iframe()

```

<div>
<img src="https://github.com/Piettro314/Identifying-and-addressing-outliers-/blob/main/media%20content/ydataProfile.png" align="center" width="100%">
</div>

# Further analysis

A boxplot diagram is then utilized to conduct a more detailed examination of the skewed data that was identified using the ydata_profiling library.

<div>
<img src="https://github.com/Piettro314/Identifying-and-addressing-outliers-/blob/main/media%20content/Box%20plot%20original.png" align="center" width="100%">
</div>

After the identification of the outliers, the subsequent code was utilized to eliminate and preserve them in a CSV file for future analysis.

```
data_outliers = data[data['cost per night cad']>380.00]
data_outliers.shape

data= data.drop(data_outliers.index)
print(f'Data for model: {data.shape}, \nData outliers: {data_outliers.shape}')
data_outliers.to_csv('./data/euBnB_outliers.csv', index=False)
```
### Results

<div>
<img src="https://github.com/Piettro314/Identifying-and-addressing-outliers-/blob/main/media%20content/Results.png" align="center" width="100%">
</div>

# Technologies used

* [ydata_profiling](https://pypi.org/project/ydata-profiling/)
* [pandas](https://pandas.pydata.org/)
* [seaborn](https://seaborn.pydata.org/)

# Remarks
When embarking on a data science project, it is crucial to identify any potential challenges from the dataset. While outliers may not necessarily cause significant issues in certain cases, it is still worthwhile to examine them after they have been identified to determine their potential impact on the overall outcome of the project.
