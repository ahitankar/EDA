# EDA

## 1. EDA on Tabular Data

* Pandas Profiling  [Documentation](https://pandas-profiling.ydata.ai/docs/master/index.html "Pandas Profiling")
    
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


* D Tale  [Documentation](https://pypi.org/project/dtale/ "DTale")

    One of the best EDA Library found so far. It has lot of customizations available. [Here](http://alphatechadmin.pythonanywhere.com/dtale/main/1)
* Lux   [Documentation](https://lux-api.readthedocs.io/en/latest/ "Lux")

    We can apply any command from Pandas’s API to the dataframes in Lux and expect the same behavior.

### **Conclusion**
    Generally we can classify the dataset based on volumnes:
    When the dataset is large in volumne then it's found that D-Tale take too much time to load and lux also did not show it's performance at it's best. So in that case use Pandas Profiling for large dataset so that we will get the report as a whole for analysis.

## 2. EDA on Text Data

* Texthero    [Documentation](https://texthero.org/ "Text Hero")

   It is very simple to learn and designed to be used on top of Pandas. [Click Here](https://pypi.org/project/texthero/)
