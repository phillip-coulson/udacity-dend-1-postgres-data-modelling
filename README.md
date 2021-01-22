# Introduction
There is a requirement from Sparkify to be able to analyse their Songs and User Activity data from a new streaming app. This project will aim to create a Postgress SQL database to service the required data to it's users. 

# Data Model
A Star Schema data model has been agreed that has the below FACT and DIMENSION tables:

## Fact Table
songplays - records in log data associated with song plays i.e. records with page NextSong

## Dimension Tables
users - users in the app
songs - songs in music database
artists - artists in music database
time - timestamps of records in songplays broken down into specific units

# Source Data
The purpose of this project is to load records from the below data sources into the database:
- Log files : /data/log_data/{YYYY}/{MM}/{YYYY-MM-DD}-events.json
- Song files: /data/song_data/*/*/{ID}.json

# Execution
There are 2 x files that can be executed using the below syntax:
1. python create_tables.py 
    This will inniate a connection to the sql server database (studentdb) and create a new database (sparkifydb). If an existing database already exists, this will be torn down.
    This will then run a series of DROP TABLE statements from sql_queries.py to ensure that any existing tables with the required names are dropped.
    This will then run a DDL (series of CREATE TABLE statements also from sql_queries.py) to define and create the required tables within the database
    All SQL code being run can be found in /sql_queries.py
2. python etl.py
    This will loop through any Song files in /data/song_data, and INSERT the required data into the SONG and ARTIST tables
    This will loop through any Log files in /data/log_data/, and INSERT the required data into the SONGPLAYS, USERS and TIME tables
    