# Data Analysis and Visualization of World Development Indicators

This project involves analyzing and visualizing the World Development Indicators (WDI) dataset from the World Bank. The primary goal is to extract insights and trends from various development indicators across different countries over the years.

## Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

- Python 3.8
- pandas
- seaborn
- matplotlib
- numpy

### Installation

1. Clone the repo:
    ```sh
    git clone https://github.com/dipitvasdev/Data-Analysis-World-Development-Indicators-in-Python.git
    ```
2. Install the required packages:
    ```sh
    pip install pandas seaborn matplotlib numpy
    ```

## Usage

1. Download the WDI dataset in CSV format from the [World Bank website](https://datacatalog.worldbank.org/search/dataset/0037712/World-Development-Indicators).
2. Extract the downloaded `WDI_CSV.zip` file to get the `WDICSV.csv`.
3. Place the `WDIData.csv` file in the project directory.

4. Run the `Data_Analysis_and_Visualisation_WDI_Dataset.ipynb` python notebook to start the analysis:

### Script Overview

The script performs the following steps:

1. **Importing Necessary Libraries**
    ```python
    from zipfile import ZipFile
    import pandas as pd
    import seaborn as sns
    import matplotlib.pyplot as plt
    import numpy as np
    ```

2. **Extracting and Loading the Dataset**
    ```python
    with ZipFile("WDI_CSV.zip", "r") as zip:
        zip.extractall("WDI_CSV")
    df = pd.read_csv("WDI_CSV/WDIData.csv")
    df.head(n=5)
    ```

3. **Preprocessing the Data**
    ```python
    df.drop_duplicates(inplace=True)
    df = df.drop(columns=["Unnamed: 66"])
    df.info()
    ```

4. **Data Exploration and Visualization**
    - **Indicator 1: Access to clean fuels and technologies for cooking (% of population)**
        ```python
        unique_indicators = df["Indicator Name"].unique()
        indicator_1 = unique_indicators[0]
        df_indicator1 = df[df["Indicator Name"] == indicator_1]
        df_indicator1 = df_indicator1.melt(id_vars=['Country Name', 'Country Code', 'Indicator Name', 'Indicator Code'], var_name='year', value_name='value')
        line_plot = sns.lineplot(data=df_indicator1[df_indicator1["Country Name"].isin(["Arab World", "Bhutan", "India", "China", "United States"])], x="year", y="value", hue="Country Name")
        line_plot.set_xlabel("Year")
        line_plot.set_ylabel(indicator_1)
        line_plot.set_title("Trend of Indicator 1")
        plt.xticks(rotation=90)
        plt.show()
        ```

    - **Indicator 2: GDP (current US$)**
        ```python
        indicator_2 = "GDP (current US$)"
        df_indicator2 = df[df["Indicator Name"] == indicator_2]
        df_indicator2 = df_indicator2.melt(id_vars=['Country Name', 'Country Code', 'Indicator Name', 'Indicator Code'], var_name='year', value_name='value')
        line_plot = sns.lineplot(data=df_indicator2[df_indicator2["Country Name"].isin(["Arab World", "Thailand", "India", "China", "United States"])], x="year", y="value", hue="Country Name")
        line_plot.set_xlabel("Year")
        line_plot.set_ylabel(indicator_2)
        line_plot.set_title("Trend of Indicator 2")
        plt.xticks(rotation=90)
        plt.show()
        ```

    - **Additional Indicators and Visualizations**
        ```python
        indicator_3 = "Life expectancy at birth, total (years)"
        indicator_4 = "Human capital index (HCI) (scale 0-1)"
        df_indicators = df[df["Indicator Name"].isin([indicator_1, indicator_2, indicator_3, indicator_4])]
        df_indicators = df_indicators.melt(id_vars=['Country Name', 'Country Code', 'Indicator Name', 'Indicator Code'], var_name='year', value_name='value')
        sns.barplot(data=df_indicators[df_indicators["year"] == '2020'], x="Country Name", y="value", hue="Indicator Name")
        plt.xticks(rotation=90)
        plt.show()
        ```

## About Me
I am Dipit Vasdev, a highly motivated problem solver with a passion for neural networks and machine learning. I recently completed my Master's degree in Computer Engineering at New York University, and my greatest strength lies in my drive for solving complex problems in computer science. I possess a wealth of technical skills in machine learning, deep learning, Android development, and more, and I have taken part in various projects and internships to continuously improve my skills and knowledge.

🔗 [LinkedIn](https://www.linkedin.com/in/dipitvasdev)

🗣️ **Feedback**
If you have any feedback, please reach out to me at dipit.vasdev@nyu.edu.
