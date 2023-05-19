#For this projectm, I downloaded Spotify Data for Kaggle.com.
#Then I created a table to insert Spotify data into.
#Finally, I preformed analytics on the data using SQL.


CREATE TABLE BIT_DB.Spotifydata (
id integer PRIMARY KEY,
artist_name varchar NOT NULL,
track_name varchar NOT NULL,
track_id varchar NOT NULL,
popularity integer NOT NULL,
danceability decimal(4,3) NOT NULL,
energy decimal(4,3) NOT NULL,
song_key integer NOT NULL,
loudness decimal(5,3) NOT NULL,
song_mode integer NOT NULL,
speechiness decimal(5,4) NOT NULL,
acousticness decimal(6,5) NOT NULL,
instrumentalness decimal(8,7) NOT NULL,
liveness decimal(5,4) NOT NULL,
valence decimal(4,3) NOT NULL,
tempo decimal(6,3) NOT NULL,
duration_ms integer NOT NULL,
time_signature integer NOT NULL )

#Then,I inserted the Spotify Data .csv into the table.

#Next, I explored the data using the following SQL.

#First I determined the avg popularity, danceability, and energy levels by artist and track. 
SELECT 
artist_name
,track_name
,AVG(popularity)
,AVG(danceability)
,AVG(energy)
FROM BIT_DB.Spotifydata
GROUP BY artist_name,track_name

#Then I determined who the Top 10 artists are by popularity
SELECT
track_name
,artist_name
,popularity
FROM BIT_DB.Spotifydata
ORDER BY popularity DESC
LIMIT 10

#NEXT I wanted to know which artist were scored the lowest in danceability and energy levels with their songs.
SELECT
artist_name
,track_name
,MIN(danceability)
,MIN(energy)
FROM BIT_DB.Spotifydata
ORDER BY artist_name

#After I wanted to determine which tracks have different modes 0-1 that were slow beats and can have acoustic sound.
SELECT 
track_name
,song_mode
,acousticness
,duration_ms
FROM BIT_DB.Spotifydata
ORDER BY track_name
LIMIT 10

#Finally I wanted to select all the artists who have dance songs more than 0.800 amps using GROUP BY and HAVING results should include the artist
and the total amp of danceability count as dance_songs.
SELECT
artist_name
,SUM(danceability) AS dance_songs
FROM BIT_DB.Spotifydata
GROUP BY artist_name 
HAVING dance_songs >0.800
