# Video Game Sales Analysis (COMP 6150)

- [Video Game Sales Analysis (COMP 6150)](#video-game-sales-analysis-comp-6150)
	- [Introduction](#introduction)
	- [Selection of Data](#selection-of-data)
	- [Exploratory data anylysis (EDA)](#exploratory-data-anylysis-eda)

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

Data preview:
![data screenshot](/graph/data-preview.png)

![data type screenshot](/graph/data-type.png)

Looking at the image above , we can see that there are 4 categorical variables (variables with `'O'` for their datatype): `Name`, `Platform`, `Genre`. I used pandas's [factorize](https://pandas.pydata.org/docs/reference/api/pandas.factorize.html) function to get a numerical value for these variable. We can also see that `Rank` and `Name` have a high number of unique values, the percentage can be observe below:

![percentage of unique values for column Rank and Name](/graph/name-rank-unique.png)

With Rank having 100% uniqueness, I believe I will drop this as it might not prove useful to the project.

## Exploratory data anylysis (EDA)


