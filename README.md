# EDA

# 1. EDA on Tabular Data

##  Data Prep  [Documentation](https://docs.dataprep.ai/index.html "Data Prep")
---
DataPrep lets you prepare your data using a single library with a few lines of code.
Currently, you can use DataPrep to:
Collect data from common data sources (through dataprep.connector)
Do your exploratory data analysis (through dataprep.eda)
Clean and standardize data (through dataprep.clean)

DataPrep.EDA is the fastest and the easiest EDA (Exploratory Data Analysis) tool in Python. It allows you to understand a Pandas/Dask DataFrame with a few lines of code in seconds.

**Create Profile Reports, Fast**

You can create a beautiful profile report from a Pandas/Dask DataFrame with the create_report function. DataPrep.EDA has the following advantages compared to other tools:

*   **10X Faster:** DataPrep.EDA can be 10X faster than Pandas-based profiling tools due to its highly optimized Dask-based computing module.
*   **Interactive Visualization:** DataPrep.EDA generates interactive visualizations in a report, which makes the report look more appealing to end users.
*   **Big Data Support:** DataPrep.EDA naturally supports big data stored in a Dask cluster by accepting a Dask dataframe as input.
---

### Installation

`pip install dataprep`

### Import the DataPrep

`from dataprep.eda import *`


### Generate Report

```python
report = create_report(df)
report
```

### Modules of EDA in DataPrep

1.  **plot(): analyze distributions**

    plot(df): plots the distribution of each column and computes dataset statistics

    plot(df, col1): plots the distribution of column col1 in various ways, and computes its statistics

    plot(df, col1, col2): generates plots depicting the relationship between columns col1 and col2


2.  **plot_correlation(): analyze correlations**

    plot_correlation(df): plots correlation matrices (correlations between all pairs of columns)

    plot_correlation(df, col1): plots the most correlated columns to column col1

    plot_correlation(df, col1, col2): plots the joint distribution of column col1 and column col2 and computes a regression line


3.  **plot_missing(): analyze missing values**
    plot_missing(df): plots the amount and position of missing values, and their relationship between columns

    plot_missing(df, col1): plots the impact of the missing values in column col1 on all other columns

    plot_missing(df, col1, col2): plots the impact of the missing values from column col1 on column col2 in various ways.

4.  **plot_diff(): analyze differences**

    The function plot_diff() explores the difference of column distributions and statistics across multiple datasets.

5.  **create_report: generate profile reports from a pandas DataFrame**

The goal of create_report is to generate profile reports from a pandas DataFrame. create_report utilizes the functionalities and formats the plots from dataprep. It provides the following information:

1.  **Overview:** detect the types of columns in a dataframe

2.  **Variables:** variable type, unique values, distint count, missing values

3.  Quantile statistics like minimum value, Q1, median, Q3, maximum, range, interquartile range

4.  Descriptive statistics like mean, mode, standard deviation, sum, median absolute deviation, coefficient of variation, kurtosis, skewness

5.  Text analysis for length, sample and letter

6.  **Correlations:** highlighting of highly correlated variables, Spearman, Pearson and Kendall matrices

7.  **Missing Values:** bar chart, heatmap and spectrum of missing values


```python
from dataprep.eda import create_report
report = create_report(df, title='My Report')
```


### **Customizations available in dataprep.**

1.  Display: is a list of names which controls the Tabs, Sections and Sessions you want to show.

2.  Config: is a dictionary that contains the customizable parameters and designated values.

Click the question mark icon in the upper right corner of each plot, in the pop-up you will see the customizable parameters for that plot, parameters’ brief descriptions and parameters’ default settings. You can easily use the Copy All Parameters button to copy the parameters with their default settings into a dictionary. Then customize the settings and pass to the config argument.

Example 1:  Choose the Tabs, Sections and Sessions you want
```python
from dataprep.eda import plot,create_report
from dataprep.datasets import load_dataset
df = load_dataset('titanic')
plot(df, 'Pclass', display=['Stats', 'Bar Chart', 'Pie Chart'])
```
Example 2: Customize your plot. [Refer this](https://docs.dataprep.ai/api_reference/dataprep.eda.html#module-dataprep.eda.configs)
```python
plot(df, "Pclass", config={'bar.bars': 10, 'bar.sort_descending': True, 'bar.yscale': 'linear', 'height': 400, 'width': 450, })
```
Example 3: Customize your Insights
```python
plot(df,config={'insight.missing.threshold':20, 'insight.duplicates.threshold':20})
```


##  Pandas Profiling  [Documentation](https://pandas-profiling.ydata.ai/docs/master/index.html "Pandas Profiling")
---
The pandas df.describe() function is great but a little basic for serious exploratory data analysis. pandas_profiling extends the pandas DataFrame with df.profile_report() for quick data analysis.The report generated is static in nature.

####    Pandas Profiling gives the following statistics in the HTML report.

*   **Type inference:** detect the types of columns in a dataframe.
*   **Essentials:** type, unique values, missing values
*   **Quantile statistics** like minimum value, Q1, median, Q3, maximum, range, interquartile range
*   **Descriptive statistics** like mean, mode, standard deviation, sum, median absolute deviation, coefficient of variation, kurtosis, skewness
*   **Most frequent values**
*   **Histogram**
*   **Correlations** highlighting of highly correlated variables, Spearman, Pearson and Kendall matrices
*   **Missing values** matrix, count, heatmap and dendrogram of missing values
*   **Text analysis** learn about categories (Uppercase, Space), scripts (Latin, Cyrillic) and blocks (ASCII) of text data.
*   **File and Image analysis** extract file sizes, creation dates and dimensions and scan for truncated images or those containing EXIF information.

### Installation

`pip install pandas-profiling`

### Import the ProfileReport

`from pandas_profiling import ProfileReport`


### Generate Report

```python
profile = ProfileReport(df)
profile
```

### Sections of report

1.  **Overview**
The Overview consists of overall statistics. This includes the number of variables (features or columns of the dataframe), Number of observations (rows of dataframe), Missing cells,  percentage of missing cells, Duplicate rows, percentage of duplicate rows, and Total size in memory.
The warnings tab consists of any type of warnings related to cardinality, correlation with other variables, missing values, zeroes, skewness of the variables, and many others.

2.  **Variables**
This section of the report gives a detailed analysis of all the variables/columns/features of the dataset. The information presented varies depending upon the data type of variable. 
Let’s break it down.

    For **numeric** data type features, you get information about the distinct values, missing values, min-max, mean, and negative values count. You also get small representation values in the form of a Histogram.

    For **string** type variables, you get Distinct (unique) values, distinct percentage, missing, missing percentage, memory size, and a horizontal bar presentation of all the unique values with count presentation.

3. **Correlations**
Correlation is used to describe the degree to which two variables move in coordination with one another. In the pandas profiling report, you can access 5 types of correlation coefficients: Pearson’s r, Spearman’s ρ, Kendall’s τ, Phik (φk), and Cramér’s V (φc).

4. **Missing values**
The report generated also contains the visualizations for the missing values present in the dataset. You get 3 types of plot: Count, matrix, and dendrogram.

### To save the report
```
profile.to_file("Analysis.html")
profile.to_file("Analysis.json")
```

### Add Metadata 
```python
profile = ProfileReport(df,
                        title="Agriculture Data",
        dataset={
        "description": "This profiling report was generated for Analytics Vidhya Blog",
        "copyright_holder": "Analytics Vidhya",
        "copyright_year": "2021",
        "url": "https://www.analyticsvidhya.com/blog/",
    },)
profile
```
Add information about the variables used in the dataset using the variables parameter. 
```python
variables={
        "descriptions": {
            "State_Name": "Name of the state",
            "District_Name": "Name of district",
            "Crop_Year": "Year when it was seeded",
            "Season": "Crop year",
            "Crop": "Which crop was seeded?",
            "Area": "How much area was allocated to the crop?",
            "Production": "How much production?",
        }
    }
```

Control Parameters of the report
```python
profile = ProfileReport(df,
                        title="Agriculture Data",
                        correlations={
                                        "pearson": {"calculate": True},
                                        "spearman": {"calculate": False},
                                        "kendall": {"calculate": False},
                                        "phi_k": {"calculate": False},
    })
```

### Explore deeper
```python
profile = ProfileReport(df, title="Pandas Profiling Report", explorative=True)
```

### Large Datasets
This is a default configuration that disables expensive computations (such as correlations and duplicate row detection).
```python
profile = ProfileReport(large_dataset, minimal=True)
profile.to_file("output.html")
```
### Using a custom configuration file
To set the configuration of pandas-profiling using a custom file.
```python
profile = ProfileReport(df, config_file="your_config.yml")
profile.to_file("report.html")
```

### Cutomise plots
A way how to pass arguments to the underlying matplotlib is to use the plot argument. It is possible to change the default format of images to png (default svg) using the key-pair image_format: "png" and also the resolution of the image using dpi: 800. An example would be:
```python
profile = ProfileReport(
    planets,
    title="Pandas Profiling Report",
    explorative=True,
    plot={"dpi": 200, "image_format": "png"},
)
```




---

 ## D Tale  [Documentation](https://pypi.org/project/dtale/ "DTale")
---
D-Tale is the combination of a Flask back-end and a React front-end to bring you an easy way to view & analyze Pandas data structures. It integrates seamlessly with ipython notebooks & python/ipython terminals. Currently this tool supports such Pandas objects as DataFrame, Series, MultiIndex, DatetimeIndex & RangeIndex. It has lot of customizations available. [Here](http://alphatechadmin.pythonanywhere.com/dtale/main/1)

### Installation

`pip install dtale`

### Import the dtale

`import dtale`


### Generate Report

```python
d = dtale.show(df)
```
### Open Server Browser
```python
d.open_browser()
```
---
## Lux   [Documentation](https://lux-api.readthedocs.io/en/latest/ "Lux")
---
Lux is designed to be tightly integrated with Pandas and can be used as-is, without modifying your existing Pandas code. To enable Lux, simply add import lux along with your Pandas import statement.
Lux preserves the Pandas dataframe semantics – which means that you can apply any command from Pandas’s API to the dataframes in Lux and expect the same behavior. For example, we can load the dataset via standard Pandas read_* commands. To visualize your dataframe in Lux, simply print out the dataframe. You should see the default Pandas table display with an additional toggle button.


### Installation

`pip install lux-api`

### Import the dtale

`import lux`


### Generate Report

```python
df = pd.read_csv("lux/data/college.csv")
df
```
---
## **Conclusion**
---
    Generally we can classify the dataset based on volumnes:
    When the dataset is large in volumne then it's found that D-Tale take too much time to load and lux also did not show it's performance at it's best. So in that case use Pandas Profiling for large dataset with "minimal = True" so that we will get the report as a whole for analysis and then we can modify the config.yml file as per our requirement.


---
# 2. EDA on Text Data

## Texthero    [Documentation](https://texthero.org/ "Text Hero")

Texthero is a python package to work with text data efficiently.
It empowers NLP developers with a tool to quickly understand any text-based dataset and
it provides a solid pipeline to clean and represent text data, from zero to hero.

#   Texthero include tools for:

*   Preprocess text data: it offers both out-of-the-box solutions but it's also flexible for custom-solutions.
*   Natural Language Processing: keyphrases and keywords extraction, and named entity recognition.
*   Text representation: TF-IDF, term frequency, and custom word-embeddings (wip)
*   Vector space analysis: clustering (K-means, Meanshift, DBSCAN and Hierarchical), topic modeling (wip) and interpretation.
*   Text visualization: vector space visualization, place localization on maps (wip).

For detailed Implemtation refer to [this](Text%20Data/text_EDA.ipynb) notebook.
