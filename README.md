# Video Game Sales Analysis (COMP 6150)

- [Video Game Sales Analysis (COMP 6150)](#video-game-sales-analysis-comp-6150)
	- [Introduction](#introduction)
	- [Selection of Data](#selection-of-data)
		- [Data preview:](#data-preview)
		- [Data description:](#data-description)
		- [Exploraty Data Analysis (EDA)](#exploraty-data-analysis-eda)
			- [Numerical Variable EDA](#numerical-variable-eda)
				- [Rank](#rank)
				- [Year](#year)
				- [NA\_Sales](#na_sales)
				- [EU\_Sales](#eu_sales)
				- [JP\_Sales](#jp_sales)
				- [Other\_Sales](#other_sales)
				- [Global\_Sales](#global_sales)
			- [Categorical Variable EDA](#categorical-variable-eda)
				- [Platform](#platform)
				- [Genre](#genre)
				- [Publisher](#publisher)
			- [Feature Engineering](#feature-engineering)
				- [Handling NaN](#handling-nan)
				- [Handling Skewness](#handling-skewness)
				- [Removing Rank](#removing-rank)
				- [Correlation](#correlation)
	- [Methods](#methods)
	- [Results](#results)
		- [Question 1:](#question-1)

## Introduction

The goal of this project is to use my knowledge acquired from this class and perform some simple data analysis on a dataset about video game sales. The reason I chose a video game sales dataset is that I love to play video games and have an interest in game development. I wanted to use this project as an excuse to do some investigation on game development, finding out what makes or breaks a game.

## Selection of Data

The processing of the data are conducted using Jupyter Notebok and is available [here](code/VideoGameSales_Analysis.ipynb).

The dataset selected contain sales data for video games from the year 1980 to 2020. The dataset have about 16,000 samples with 11 features:

* Rank
* Name
* Platform
* Year
* Genre
* Publisher
* NA_Sales
* EU_Sales
* JP_Sales
* Other_Sales
* Global_Sales

The objective of this project is to answers these 3 question:
1. Which platform has the highest game sales?
2. Which column affect sales the most?
3. Which year has the highest amount of game sales?

The dataset can be found at [kaggle](https://www.kaggle.com/datasets/gregorut/videogamesales) [1].

### Data preview:
![data screenshot](/graph/data-preview.png)

![data type screenshot](/graph/data-type.png)

Looking at the image above , we can see that there are 4 categorical variables (variables with `'O'` for their datatype): `Name`, `Platform`, `Genre`. I used pandas's [factorize](https://pandas.pydata.org/docs/reference/api/pandas.factorize.html) function to get a numerical value for these variable. We can also see that `Rank` and `Name` have a high number of unique values, the percentage can be observe below:

![percentage of unique values for column Rank and Name](/graph/name-rank-unique.png)

With Rank having 100% uniqueness, I believe I will drop this as it might not prove useful to the project.

### Data description:

![Data description](/graph/data-describe.png)

Using the output above, we can determine a few things, using `count`, we can find out if there is any data lost in those variables and by comparing the `mean` and median (`50%`) we can see determine the skewness of the data. Based on `count`, Year seems to be the only one with some minor data lost while the other are fine. Checking for right skewness, we can see that for all the sales columns (`NA_Sales`, `EU_Sales`, `JP_Sales`, `Other_Sales`, `Global_Sales`) the `mean` is **greater** than the median(`50%`), which mean the data is right skewed.

### Exploraty Data Analysis (EDA)

Here I will take a closer look at the data set to find any pattern that exist in the dataset. First, I will split the columnns into two types, `numerical` and `categorical` variables.

Here is the list of columns split into those types:
![list of numerical and categorical variables](/graph/num-cat-var-list.png)

#### Numerical Variable EDA

Here I will perform a histogram plot, using `seaborn`, which plot univariate or bivariate histogram to show the distribution of datasets. It is able to do this by counting the number of observation that fall within discrete bins.

##### Rank

![histplot for rank](/graph/rankEDA.png)

##### Year

![histplot for year](/graph/yearEDA.png)

##### NA_Sales

![histplot for NA_Sales](/graph/NA_SalesEDA.png)

##### EU_Sales

![histplot for EU_Sales](/graph/EU_SalesEDA.png)
##### JP_Sales

![histplot for JP_Sales](/graph/JP_SalesEDA.png)

##### Other_Sales

![histplot for Other_Sales](/graph/Other_SalesEDA.png)

##### Global_Sales

![histplot for Global_Sales](/graph/Global_SalesEDA.png)

Ealier, in [data describtion](#data-description), I theorize that there are some right skewness for the 5 sales columns and these graph above further reinforce my theory.

#### Categorical Variable EDA

For this section, I will use barplot and countplots. The barplot will be use to represents a statistical estimate for a variable with the height of each recatangle and indicates the uncertanty around that estimate using an error bar. A count plot is similar to a histogram but across a categorical instead of quantitative variable, it show the counts of observation in each categorical bin using bars.

##### Platform

![Barplot for Platform](/graph/platformEDA.png)

Here I wanted to see if there were any genre that sold better on different platform

![Barplot for Platform, seprated by Genre](/graph/platform-genreEDA.png)

We can see that some genres are more popular in certain platforms, for examples: Shooters games are the most popular on the NES.

##### Genre

![Barplot for Genre](/graph/genreEDA.png)

##### Publisher

![Barplot for Publisher](/graph/publisherEDA.png)

This plot here is a bit harder to look at because of the number of unique publisher and the scale which `seaplot` would allow me to plot.

#### Feature Engineering

Here I will be perform a few operation to make the dataset easier to use and expose patterns in the dataset.

##### Handling NaN

![A picture showing the percantage of NaN in each column](/graph/NaNPercent.png)

Looking at the graph above, `Year` and `Publisher` have a small amount of Not a Number(NaN) values. I will try to eliminate this by imputing the NaN with the most common value (Modes). Since the percentage of NaN is very small, I do not belive this will have large affect on the statistical data.

![Code of imputing NaN with modes](/graph/NaN-mode.png)

##### Handling Skewness

Earlier, in the [Numerical Variable EDA](#numerical-variable-eda), we saw that NA, EU, JP, Other, and Global Sales suffer from right skewness, I intend on fixing this by applying log transformation on these columns.

**Before**:

![Data description](/graph/data-describe.png)

**After**:

![Data description but logged](/graph/datalogged.png)

Comparing the before and after graph, we can see that the sales columns are a lot less skewed.

##### Removing Rank

I believe that rank does not provide much statistical data since it server as a weird index. As a result, I will be removing it.

![Code for removing rank](/graph/removeRank.png)

##### Correlation

For this section, I will fecotrice the dataset and create a correlation heatmap to find correlation between each column in the dataset.

![correlation graph](/graph/correlation.png)

## Methods

**Tools**:

*	Numpy, Matplotlib, Seaborn, and Pandas for data analysis and transformation.
*	GitHub for version control
*	Google Colab as an IDE for Jupyter notebook
*	VS Code as an IDE for the rest of the project

**Features**:

* Imputing NaN with Modes:
  * There are many ways to handle NaN in a dataset, while there are not many NaN in this dataset, `Year` and `publisher` still contain a small percantage of NaN which can be seen [here](#handling-nan). To resolve this, I chose to impute the NaN with Modes, the most common values in the column, which should not add too much statistical data to the dataset since there are only some NaN values.
  * This was achive by using a loop through the columns with NaN (`Year`, `Publisher`), using Panda's [fillna](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.fillna.html) method and [mode](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.mode.html#pandas.DataFrame.mode) method, I then fill each NaN with the mode of that column.
* Handling Skewness:
  * This process was relatively painless, I used Numpy's [log1p](https://numpy.org/doc/stable/reference/generated/numpy.log1p.html) function on the affected column and this was able to improve the skewness. The reason behind this is that Logarithmic transformation can help normalize positively skewed data, which it was, and help make it more symmetrical and easier to anaylize
* Correlation
  * This method was used to determine the relationship of the columns with `Global_Sales` in order to answer question 1 and 2.
  * To start, I had to factorize the dataset in order to get a meaningfull numeric value out of the categorical value, making the correlation possible, this was done using Panda's [apply](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.apply.html#pandas.DataFrame.apply) method to apply a small lambda function, which use Panda's [factorize](https://pandas.pydata.org/docs/reference/api/pandas.factorize.html#pandas-factorize) function on each value of the dataset. Next I use Panda's [corr](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.corr.html#pandas.DataFrame.corr) function to create a correlation matrix of the dataset which is then graphed using seaborn's [heatmap](https://seaborn.pydata.org/generated/seaborn.heatmap.html#seaborn.heatmap)
## Results

### Question 1: 

According to the graph
