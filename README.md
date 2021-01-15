## Discuss the purpose of this database in the context of the startup, Sparkify, and their analytical goals.

The purpose of this database is to be able to analyse how Sparkify is being used by it's users. It has been decided to transform the data and load it into an postgresql database as traversing directories and doing analysis on json text files is not the easiest and especially as any analysis code would be tied to this storage format which could easily change in a few years. With this information easily available it will be possible for them to maybe tailor their user interface for their users depending on location. Or even build recomended playlists based on the user's previous listening activity.

The company also wants a central place to store all this information as keeping the information in different directories can become cumbersome and hard to maintain.

## State and justify your database schema design and ETL pipeline.

We have a fact table called Songplays and dimension tables named users, artists, songs and time. Songplays has been used as a fact table as the main entity/event the company is interested in is the actual streaming of a song (a songplay). This will make it very quick to execute queries on song streams and only require joins if additional information such as artist/song name are needed. Python with Pandas was used in the ETL as it makes it very quick to select/filter out certain information.

## Example queries

### Check the most played songs in order

select song_id, count(song_id) from songplays group by song_id order by count(song_id) desc

### Check the most played artists
select artist_id, count(artist_id) from songplays group by artist_id order by count(artist_id) desc

## Running the project

Run script "create_tables.py" 
Run script "etl.py" 

"create_tables.py" will drop any existing tables and crecreate the table to give you a fresh environment. 
"etl.py" script will then traverse the log_data and song_data directories and transform the data from the json files contained in these directories into the postgresql database tables we have created and populate them. 