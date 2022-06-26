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

*note : [how to upload large files to GitHub repository](https://medium.com/linkit-intecs/how-to-upload-large-files-to-github-repository-2b1e03723d2)*
<br/>
<br/>
## Process Overview
**Write an ETL function to read three data files** <br/>
The function takes the Wikipedia JSON file, the Kaggle metadata and MovieLens csv files and creates three separate DataFrames. <br/>

**Extract and Transform the Wikipedia data** <br/>
We filtered out the TV shows, consolidated the redundant data, removed the duplicates and formatted the Wikipedia data, to achieve desired form.<br/>

**Extract and Transform the Kaggle and rating data** <br/>
The same process, we consolidated the redundant data, removed the duplicates, formatted and grouped the data. The Kaggle and rating data were then merged with the Wikipedia movies DataFrame.<br/>

-------------------------------------------
Transform and merge the ratings DataFrame:
-------------------------------------------

    from sqlalchemy import create_engine
    from config import db_password
    !pip install psycopg2
    
    # Create the Database Engine - local server, the connection string will be as follows:
    db_string = f"postgres://postgres:{db_password}@127.0.0.1:5432/movie_data"
    
    # Create the database engine (to the PostgreSQL database)
    engine = create_engine(db_string)
    
    # Import the movies_df DataFrame to a SQL database.
    movies_df.to_sql(name='movies', if_exists='replace',con=engine)
    
    # Create a variable rows_imported
    rows_imported = 0
    
    # Set start_time from time.time()
    start_time = time.time()

    for data in pd.read_csv(f'{file_dir}/ratings.csv', chunksize=1000000):

        # Print out the range of rows
        print(f'importing rows {rows_imported} to {rows_imported + len(data)}...', end='')

        data.to_sql(name='ratings', con=engine, if_exists='append')

        # Increment the numb. rows imported
        rows_imported += len(data)

        # Final print out
        print(f'Done. {time.time() - start_time} total seconds elapsed')
        
 <br/>

**Load the data to a PostgreSQL Database** <br/>
<br/>
![load.png](Resources/load.png)
<br/>
<br/>
**The Total Number of Rows Loaded Into Database** <br/>

![movies_query.png](Resources/movies_query.png)
<br/>
![ratings_query.png](Resources/ratings_query.png)
<br/>
<br/>

## Summary
The ETL function collects and cleans movie data from different sources (Wikipedia JSON and Kaggle and ratings csv files). It transforms and merges the data and loads it into two updatable PostgreSQL dataset tables ready to be used by the hackathon participants for their analysis.<br/>

