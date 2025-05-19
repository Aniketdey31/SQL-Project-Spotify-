![Spotify Logo](https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/blob/main/spotify_logo.jpg)
# Spotify SQL Project and Query Optimization
Project Category: Advanced
[Click Here to get Dataset](https://www.kaggle.com/datasets/sanjanchaudhari/spotify-dataset)

## Overview
This project involves analyzing a Spotify dataset with various attributes about tracks, albums, and artists using **SQL**. It covers an end-to-end process of normalizing a denormalized dataset, performing SQL queries of varying complexity (easy, medium, and advanced), and optimizing query performance. The primary goals of the project are to practice advanced SQL skills and generate valuable insights from the dataset.

## Project Steps

### 1. Data Exploration
Before diving into SQL, it’s important to understand the dataset thoroughly. The dataset contains attributes such as:
- `Artist`: The performer of the track.
- `Track`: The name of the song.
- `Album`: The album to which the track belongs.
- `Album_type`: The type of album (e.g., single or album).
- Various metrics such as `danceability`, `energy`, `loudness`, `tempo`, and more.

### 2. Querying the Data
After the data is inserted, various SQL queries can be written to explore and analyze the data. Which includes-
1. **Simple data retrieval, filtering, and basic aggregations.**
2. **More complex queries involving grouping, aggregation functions, and joins.**
3. **Nested subqueries, window functions, CTEs, and performance optimization.**

### 3. Query Optimization
In advanced stages, the focus shifts to improving query performance. Some optimization strategies include:
- **Indexing**: Adding indexes on frequently queried columns.
- **Query Execution Plan**: Using `EXPLAIN ANALYZE` to review and refine query performance.
  
---

## 15 Questions with solutions

1. Retrieve the names of all tracks that have more than 1 billion streams.
```
SELECT 
	track, stream 
FROM spotify
WHERE stream> 1000000000;
```
2. List all albums along with their respective artists.
```
SELECT 
	album, artist  
FROM spotify
GROUP BY album, artist;
```
3. Get the total number of comments for tracks where `licensed = TRUE`.
```
SELECT 
	SUM(comments) AS total_com
FROM spotify
WHERE licensed = 'TRUE';
```
4. Find all tracks that belong to the album type `single`.
```
SELECT 
	track 
FROM spotify
WHERE album_type= 'single';
```
5. Count the total number of tracks by each artist.
```
SELECT 
	artist,
	COUNT(track) AS no_of_tracks
FROM spotify
GROUP BY artist;
```
6. Calculate the average danceability of tracks in each album.
```
SELECT 
	album,
	AVG(danceability) AS avg_danceability
FROM spotify
GROUP BY album;
```
7. Find the top 5 tracks with the highest energy values.
```
SELECT 
	track,
	energy
FROM spotify
ORDER BY energy DESC
LIMIT 5;
```
8. List all tracks along with their views and likes where `official_video = TRUE`.
```
SELECT 
	track,
	views,
	likes
FROM spotify
WHERE official_video= 'true';
```
9. For each album, calculate the total views of all associated tracks.
```
SELECT 
	album,
	SUM(views) AS total_views
FROM spotify
GROUP BY album;
```
10. Retrieve the track names that have been streamed on Spotify more than YouTube.
```
SELECT 
	track
FROM spotify
WHERE most_played_on= 'Spotify';
```
11. Find the top 3 most-viewed tracks for each artist using window functions.
```
SELECT 
	RANK() OVER(PARTITION BY artist ORDER BY views DESC ),
	track,
	artist,
	views
FROM spotify
limit 3;
```
12. Write a query to find tracks where the liveness score is above the average.
```
SELECT 
	track, 
	liveness
FROM spotify
WHERE liveness > (SELECT 
			AVG(liveness) 
		  FROM spotify);
```
13. **Use a `WITH` clause to calculate the difference between the highest and lowest energy values for tracks in each album.**
```
WITH cte
AS(
SELECT 
	album,
	MAX(energy) AS highest_energy,
	MIN(energy) AS lowest_energy
FROM spotify
GROUP BY album
)
SELECT 
	album,
	highest_energy-lowest_energy AS energy_diff
FROM cte
order by energy_diff DESC;
```
14. Find tracks where the energy-to-liveness ratio is greater than 1.2.
```
SELECT 
	track,
	energy_liveness
FROM spotify
WHERE energy_liveness > 1.2;
```
15. Calculate the cumulative sum of likes for tracks ordered by the number of views, using window functions.
```
SELECT 
	track,
	views,
	SUM(likes) OVER(PARTITION BY track ORDER BY views DESC) AS cumulative_sum_of_likes
FROM spotify;

```

**THANK YOU**
