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
	- [Question 1: Does a platform affect game sales?](#question-1-does-a-platform-affect-game-sales)
	- [Question 2: Is there a correlation between game genre and game sales?](#question-2-is-there-a-correlation-between-game-genre-and-game-sales)
	- [Question 3: Which year sold the most games?](#question-3-which-year-sold-the-most-games)
- [Discussion](#discussion)
- [Summary](#summary)
- [References](#references)

## Introduction

The goal of this project is to use my knowledge acquired from this class and perform some simple data analysis on a dataset about video game sales. The reason I chose a video game sales dataset is that I love to play video games and have an interest in game development. I wanted to use this project to educate myself on game development and learn what it takes to develope a successful game.

## Selection of Data

The processing of this data is conducted using Jupyter Notebook and is available [here](code/VideoGameSales_Analysis.ipynb).

The dataset selected contains sales data for video games from the year 1980 to 2020. The dataset has roughly 16,000 samples with 11 features:

* Rank: A rating for the video game, it goes from 1 (highest) to 16600.
* Name: The name of the video game.
* Platform: A computer system that the game was made for.
* Year: The year the game was released.
* Genre: A specific category that the game share similar characteristics with, i.e., Horror, Adventure, Comedy.
* Publisher: The entity that sponser the video game's developer.
* NA_Sales: The ammount of money this game made in North America (in millions).
* EU_Sales: The ammount of money this game made in Europian Union (in millions).
* JP_Sales: The ammount of money this game made in Japan (in millions).
* Other_Sales: The ammount of money this game made from other regions of the world (in millions).
* Global_Sales:  The ammount of money this game made Globally (in millions).

The objective of this project is to answer these 3 questions:
1. Does a platform affect game sales?
2. Which column in my data set has the biggest affect on global sales?
3. Which year has the highest amount of game sales?

The dataset can be found at [kaggle](https://www.kaggle.com/datasets/gregorut/videogamesales) [1].

### Data preview:
![data screenshot](/graph/data-preview.png)

![data type screenshot](/graph/data-type.png)

Looking at the image above , we can see that there are 4 categorical variables (variables with `'O'` for their datatype): `Name`, `Platform`, `Genre`. I used pandas's [factorize](https://pandas.pydata.org/docs/reference/api/pandas.factorize.html) function to get a numerical value for these variables. We can also see that `Rank` and `Name` have a high number of unique values. This percentage can be observed below:

![percentage of unique values for column Rank and Name](/graph/name-rank-unique.png)

With Rank having 100% uniqueness, I believe that dropping the rank column will be beneficial to the project because it does not provide enough statistical value to answer the three questions above.

### Data description:

![Data description](/graph/data-describe.png)

Using the output above, we can determine if the dataset is right skewed and if there are any datalost. First, with `Count`, if the number of count is less than 16598, then that means there are data lost which only `Year` seems to suffer from. Next, we can determind right skewness using `mean` and median (`50%`). If `mean` is greater than `median` it means those columns are right skewed which the sales columns seems to suffer from.

### Exploraty Data Analysis (EDA)

Here I will take a closer look at the data set to find any pattern that exists in the dataset. First, I will split the columnns into two types, `numerical` and `categorical` variables.

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

For this section, I will use barplot and countplots. The barplot will be used to represents a statistical estimate for a variable with the height of each recatangle and indicates the **uncertanty** around that estimates an error bar. A count plot is similar to a histogram but across a categorical instead of quantitative variable, it shows the counts of observation in each categorical bin using bars.

##### Platform

![Barplot for Platform](/graph/platformEDA.png)

Here I wanted to see if there were any genres that sold better on different platforms.

![Barplot for Platform, seprated by Genre](/graph/platform-genreEDA.png)

We can see that some genres are more popular in certain platforms, for examples: Shooters games are the most popular on the NES.

##### Genre

![Barplot for Genre](/graph/genreEDA.png)

##### Publisher

![Barplot for Publisher](/graph/publisherEDA.png)

This plot here is a bit harder to look at because of the number of unique publishers and the scale which `seaplot` would allow me to plot.

#### Feature Engineering

Here I will perform a few operations to make the dataset easier to use and expose patterns in the dataset.

##### Handling NaN

![A picture showing the percantage of NaN in each column](/graph/NaNPercent.png)

Looking at the graph above, `Year` and `Publisher` have a small amount of Not a Number(NaN) values. I will try to eliminate this by imputing the NaN with the most common value (Modes). Since the percentage of NaN is very small, I do not belive this will have a large affect on the statistical data.

![Code of imputing NaN with modes](/graph/NaN-mode.png)

##### Handling Skewness

Earlier, in the [Numerical Variable EDA](#numerical-variable-eda), we saw that NA, EU, JP, Other, and Global Sales suffer from right skewness, I intend on fixing this by applying log transformation on these columns.

**Before**:

![Data description](/graph/data-describe.png)

**After**:

![Data description but logged](/graph/datalogged.png)

Comparing the before and after graph, we can see that the sales columns are a lot less skewed.

##### Removing Rank

I believe that rank does not provide much statistical data since it servers as a weird index. As a result, I will be removing it.

![Code for removing rank](/graph/removeRank.png)

##### Correlation

For this section, I will factorize the dataset and create a correlation heatmap to find correlation between each column in the dataset.

![correlation graph](/graph/correlation.png)

## Methods

**Tools**:

*	Numpy, Matplotlib, Seaborn, and Pandas for data analysis and transformation.
*	GitHub for version control
*	Google Colab as an IDE for Jupyter notebook
*	VS Code as an IDE for the rest of the project

**Features**:

* Imputing NaN with Modes:
  * There are many ways to handle NaN in a dataset, while there are not many NaN in this dataset, `Year` and `publisher` still contain a small percentage of NaN which can be seen [here](#handling-nan). To resolve this, I chose to impute the NaN with Modes, the most common values in the column, which should not add too much statistical data to the dataset since there are only some NaN values.
  * This was achieved by using a loop through the columns with NaN (`Year`, `Publisher`), using Panda's [fillna](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.fillna.html) method and [mode](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.mode.html#pandas.DataFrame.mode) method, I then fill each NaN with the mode of that column.
* Handling Skewness:
  * I used Numpy's [log1p](https://numpy.org/doc/stable/reference/generated/numpy.log1p.html) function on the affected column and this was able to improve the skewness. The reason behind this is that Logarithmic transformation can help normalize positively skewed data, which it was, and help make it more symmetrical and easier to analyze.
* Correlation coefficient:
  * This method is used to measure the strength of a linear relationship between two variables. Its value can range from -1 to 1. The value can be interpreted in two parts:
    * Sign: if the value is negative, when one variable changes, the other changes in the opposite direction. If the value is positive, when one variable changes, the other changes in the same direction
    * Absolute value: This indicates how much one variable will change if the other changes.
  * This method was used to determine the relationship of the columns with `Global_Sales` to answer questions 1 and 2.
  * To start, I had to factorize the dataset to get a meaningful numeric value out of the categorical value, making the correlation possible, this was done using Panda's [apply](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.apply.html#pandas.DataFrame.apply) method to apply a small lambda function, which use Panda's [factorize](https://pandas.pydata.org/docs/reference/api/pandas.factorize.html#pandas-factorize) function on each value of the dataset. Next, I use Panda's [corr](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.corr.html#pandas.DataFrame.corr) function to create a correlation matrix of the dataset which is then graphed using seaborn's [heatmap](https://seaborn.pydata.org/generated/seaborn.heatmap.html#seaborn.heatmap)
## Results

### Question 1: Does a platform affect game sales?

This question can be answered by looking at the [correlation graph](#correlation), We can see that there is a 0.1 correlation between `platform` and `Global_Sales`, meaning that as `platform` changes in a direction, `Global_Sales` will also change in the same direction by 0.1 unit, comparing to other value, this is very low. As a result, I believe that a platform has very little effect on game sales.

### Question 2: Is there a correlation between game genre and game sales?

Here game sales are interpreted as `Global_Sales`, This question can also be answered using the [correlation graph](#correlation). We can see that `genre` has a 0.08 correlation with `Global_Sales`. This means that as `genre` changes in a direction, so those `Global_Sales` by 0.08 in the same direction which is not much. With this, I believe that Genre has very little effect on game sales

### Question 3: Which year sold the most games?

For this question, I found the answer by performing a [groupby](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html) using `year` and then performing a [sum](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.sum.html). This return the sum of all `Global_Sales` grouped by year. All that is left is to find the year with the highest sales which can be seen below:

![code to find max sales and result](/graph/maxSales.png)

As we can see, for this dataset, 2008 has the highest amount of video games sold.

## Discussion

After finding a result, I feel like it was a little weird how there is not that much correlation between Platform and Game Sales. From personal experience, I have always noticed that games on console-like devices (PlayStation, Xbox, and Nintendo Switch, etc.), are more accessible than PC Games, there should be more games sold on those platforms. Having said that, the dataset proved me wrong.

Some complications that I noticed, while working on the [EDA](#exploraty-data-analysis-eda) section, many of my graphs came out looking horrible. An example would be the graph of [`publisher` vs `Global_Sales`](#publisher). Since columns like `publisher` and `name` inherently contain a lot of unique values, it might have been too much for `seaborn` and `matplotlib` to fit all of them on the x-axis. I would like to spend more time outside of the project trying to fix this problem.

## Summary

The purpose of this project is to take a look at video game sales globally from the year 1980 to 2020 and find the answers to three main questions listed [here](#selection-of-data). The dataset had some problems like right skewness and missing data which was handled using the method listed in [this](#feature-engineering). After experimenting, the answers to the question were found and they are as follows:

1. Platforms have very little effect on game sales.
2. There is some correlation between genre and game sales but not enough for any statistical purposes.
3. The year 2008 has the highest sales in games.

## References

[1] [Videogame sales dataset](https://www.kaggle.com/datasets/gregorut/videogamesales)
