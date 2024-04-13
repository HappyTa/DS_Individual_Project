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