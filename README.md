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

## Authors

- Joshua Tice
- The Udacity Team
