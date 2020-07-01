# Data Modeling with Apache Cassandra


## Objective

The goal of this project is to create an Apache Cassandra database for a simulated music streaming service called Sparkify to query on song play data. The raw data is CSV files in the event_data directory, and we will build a ETL pipeline to transform the raw data into the Apache Cassandra database.


## Data

The CSV files in Event Data ( `event_data/<yyyy>-<mm>-<dd>-events.csv` where `<yyyy>` indicates the year, `<mm>` indicates the month and `<dd>` indicates the year) has the following entries:
- artist (string)
- auth (string)
- firstName (string)
- gender (char)
- itemInSession (int)
- lastName (string)
- length (float)
- level (string)
- location (string)
- method (string)
- page (string)
- registration (float)
- sessionId (int)
- song (string)
- status (int)
- ts (float)
- userId (int)


## ETL Pipeline

1. Read in the csv data files
2. For each row of the csv data, insert the data in a column and write a new file Event_datafile_new.csv with the following entries: ['artist', 'firstName', 'gender',  'itemInSession', 'lastName', 'length', 'level', 'location', 'sessionId', 'song', 'userId']


## Queries

For NoSQL databases, we design the database based on the queries we know we want to perform. For this project, we have three queries:

1. Find artist, song title and song length that was heard during sessionId=338, and itemInSession=4.
    - `SELECT artist, song, length from table_1 WHERE sessionId=338 AND itemInSession=4`
2. Find name of artist, song (sorted by itemInSession) and user (first and last name) for userid=10, sessionId=182.
    - `SELECT artist, song, firstName, lastName FROM table_2 WHERE userId=10 and sessionId=182`
3. Find every user name (first and last) who listened to the song 'All Hands Against His Own'.
    - `SELECT firstName, lastName WHERE song='All Hands Againgst His Own'`


## Tables

For the first query: 
- Column 1 = sessionId
-  Column 2 = itemInSession
-  Column 3 = artist
-  Column 4 = song_title
-  Column 5 = length
-  Primary key = (sessionId, itemInSession)

For the second query:
- Column 1 = userId
- Column 2 = sessionId
- Column 3 = itemInSession
- Column 4 = artist
- Column 5 = song_title
- Column 6 = firstName
- Column 7 = lastName
- Primary key = (userId, sessionId) with clustering column itemInSession

For the third query:  
- Column 1 = song
- Column 2 = sessionId
- Column 3 = itemInSession
- Column 4 = firstName
- Column 5 = lastName
- Primary key = (song), session_id, item_inSession


## Build Instructions

Run Part I and Part II of `Project_1B_Project_Template.ipynb`for ETL and Cassandra Database creating and queries respectively.
