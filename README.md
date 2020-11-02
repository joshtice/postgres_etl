# Sparkify ETL Pipeline

## Summary

To support the Sparkify Data Analytics team, a data pipeline was developed to extract user activity from JSON logs and then transform and load the data into a PostgreSQL database. The database utilizes a star schema to optimize the data for querying.

## Usage

The ETL pipeline requires python 3.6, a local instance of PostgreSQL, and the raw JSON data files stored in a child directory named "data". Given this environment, the following steps can be executed to set up the ETL pipeline:  

- Install required python libraries: ```pip install -r requirements.txt```
- Instantiate the database with appropriate schema: ```python create_tables.py```
- Extract, transform, and load data into the database ```python etl.py```

## File Descriptions

- README.md: This file, which contains documentation of the ETL pipeline
- requirements.txt: Third-party python library dependencies
- etl.ipynb: Exploratory jupyter notebook for developing the ETL pipeline
- test.ipynb: Jupyter notebook for testing the ETL pipeline
- sql_queries.py: SQL queries used to drive the main steps of the ETL pipeline
- create_tables.py: Python code to generate the database and relations used to persist data. This file depends on many of the SQL queries laid out in sql_queries.py
- etl.py: The production ETL script that drives the pipeline

## Database Schema

The Sparkify database consists of five tables, whose schemata are outlined below:

### artists table
```
  Column   |       Type        | Modifiers 
-----------+-------------------+-----------
 artist_id | character varying | not null
 name      | character varying | not null
 location  | character varying | 
 latitude  | numeric           | 
 longitude | numeric           | 
Indexes:
    "artists_pkey" PRIMARY KEY, btree (artist_id)
Referenced by:
    TABLE "songplays" CONSTRAINT "songplays_artist_id_fkey" FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
```

### songplays table
```
   Column    |       Type        |                            Modifiers                            
-------------+-------------------+-----------------------------------------------------------------
 songplay_id | integer           | not null default nextval('songplays_songplay_id_seq'::regclass)
 start_time  | bigint            | not null
 user_id     | integer           | not null
 level       | character varying | not null
 song_id     | character varying | 
 artist_id   | character varying | 
 session_id  | integer           | not null
 location    | character varying | 
 user_agent  | character varying | 
Indexes:
    "songplays_pkey" PRIMARY KEY, btree (songplay_id)
Foreign-key constraints:
    "songplays_artist_id_fkey" FOREIGN KEY (artist_id) REFERENCES artists(artist_id)
    "songplays_song_id_fkey" FOREIGN KEY (song_id) REFERENCES songs(song_id)
    "songplays_user_id_fkey" FOREIGN KEY (user_id) REFERENCES users(user_id)
```

### songs table
```
  Column   |       Type        | Modifiers 
-----------+-------------------+-----------
 song_id   | character varying | not null
 title     | character varying | not null
 artist_id | character varying | not null
 year      | integer           | not null
 duration  | numeric           | not null
Indexes:
    "songs_pkey" PRIMARY KEY, btree (song_id)
Referenced by:
    TABLE "songplays" CONSTRAINT "songplays_song_id_fkey" FOREIGN KEY (song_id) REFERENCES songs(song_id)
```   
    
### time table
```
   Column   |       Type        | Modifiers 
------------+-------------------+-----------
 start_time | bigint            | not null
 hour       | integer           | not null
 day        | integer           | not null
 week       | integer           | not null
 month      | integer           | not null
 year       | integer           | not null
 weekday    | character varying | not null
Indexes:
    "time_pkey" PRIMARY KEY, btree (start_time)
```    

### users table
```
   Column   |       Type        | Modifiers 
------------+-------------------+-----------
 user_id    | integer           | not null
 first_name | character varying | not null
 last_name  | character varying | not null
 gender     | character varying | 
 level      | character varying | not null
Indexes:
    "users_pkey" PRIMARY KEY, btree (user_id)
Referenced by:
    TABLE "songplays" CONSTRAINT "songplays_user_id_fkey" FOREIGN KEY (user_id) REFERENCES users(user_id)
```

## Authors

- Joshua Tice
- The Udacity Team
