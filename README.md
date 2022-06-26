# Movies-ETL

A project in performing an ETL ( Extract, Transform, Load ) process to create data pipelines using Python, Pandas and PostgreSQL using very large data files.

## Overview
The purpose of this project was to create an automated pipeline that takes in new data, performs the appropriate transformations, and loads the data into existing tables that is connected to a database.<br/>
Within the scope of the AmazingPrime Hackathon, this project will create an automated pipeline that takes in new data from Wikipedia, Kaggle metadata and the MovieLens ratings data. It then performs the appropriate transformations and loads the data into an existing PostgreSQL database.<br/>
For this analysis, we used the following breakdown :
  1. Write an ETL function to read three data files.
  2. Extract and transform the Wikipedia data.
  3. Extract and transform the Kaggle and rating data.
  4. Load the data to a PostgreSQL Movie Database.


### Resources
  - Data sources : [wikipedia_movies.json](Resources/wikipedia-movies.json),&nbsp; [movies_metadata.csv](Resources/movies_metadata.csv),&nbsp; [Ratings.csv](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset?select=ratings.csv)
  - Softwares : [PostgreSQL](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads),&nbsp; [Python](https://www.python.org/downloads/windows/),&nbsp;  [Pandas](https://www.anaconda.com/products/distribution)

## Process Overview
**Write an ETL function to read three data files** <br/>
The function takes the Wikipedia JSON file, the Kaggle metadata and MovieLens csv files and creates three separate DataFrames. <br/>

**Extract and Transform the Wikipedia data** <br/>
We filtered out the TV shows, consolidated the redundant data, removed the duplicates and formatted the Wikipedia data, to achieve desired form.<br/>

**Extract and Transform the Kaggle and rating data** <br/>
The same process, we consolidated the redundant data, removed the duplicates, formatted and grouped the data. The Kaggle and rating data were then merged with the Wikipedia movies DataFrame.<br/>

**Load the data to a PostgreSQL Database** <br/>
<br/>
![load.png](Resources/load.png)
<br/>
![movies_quey.png](Resources/movies_quey.png)
<br/>
![ratings_query.png](Resources/ratings_query.png)
