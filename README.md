# Sparkify Data Lake Project with PySPark

A music streaming startup, Sparkify, has grown their user base and song database even more and want to move their data warehouse to a data lake. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

As their data engineer, you are tasked with building an ETL pipeline that extracts their data from S3, processes them using Spark, and loads the data back into S3 as a set of dimensional tables. This will allow their analytics team to continue finding insights in what songs their users are listening to.

You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.


## Schema Design

The tables created include one fact table, songplays and four dimensional tables namely users, songs, artists and time. This follows the star schema principle which will contain clean data that is suitable for OLAP operations which will be what the analysts will need to conduct to find the insights they are looking for.

### Fact Table

**songplays** - records in log data associated with song plays i.e. records with page NextSong

- songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

### Dimension Tables
**users** - users in the app

- user_id, first_name, last_name, gender, level

**songs** - songs in music database

- song_id, title, artist_id, year, duration

**artists** - artists in music database

- artist_id, name, location, latitude, longitude

**time** - timestamps of records in songplays broken down into specific units

- start_time, hour, day, week, month, year, weekday


## ETL Pipeline

The data gets that gets extracted will need to be transformed to to fit the data model in the target destination tables. For instance the source data for timestamp is in unix format and that will need to be converted to timestamp from which the year, month, day, hour values etc can be extracted which will fit in the relevant target time and songplays table columns. The script will also need to cater for duplicates, ensuring that they aren't part of the final data that is loaded in the tables.


## Project Files

- etl.py  - Script to execute the etl pipeline 

- dl.cfg  - AWS configurations

- test.ipynb - Notebook for testing the etl pipeline

## How to Run

### Prerequisite

- Pyspark
- Python 3 or later

### Running the Pipeline

- Setup AWS config by creating a user on your AWS account

- Set your access key and secret key in the dl.cfg file

- Run the etl.py pipeline script:
    ```
    $ python etl.py
    ```
