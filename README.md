

## Description

A TV broadcaster wants to automatically detect which music is played in each program of one of its tv channels. For that purpose is sending us an EPG (Electronic Program Guide) report file that contains:

* id
* program
* date
* time
* duration

On the other hand we can extract from our music identification service a report file that contains the songs that have been played on that chanel during the same period. This Music identification file has the following information

* identification id
* start time
* end time
* track_id
* artist
* title

The goal of the test is to build a Python script that merges the two files (Task 1). If you want to go further for some extra points, there is a bonus task (Task 2) in which you have to enrich the resulting file with metadata from an external web API. 

### Merge Files

The first step is to merge the two provided files in a single file according to time. For this task it should be taking into account that the EPG report and the Music Identification report are not perfectly synchronized, so it is possible that a track that is played at the beginning of a tv program is actually detected some seconds before in the Music Identification report. You should process those cases, so a track only coincides in time uniquely with a program. For that you should modify the track metadata, not the EPG. Example: 

| program   | date       | time     | duration | title   | start time          | end time            |
| --------- | ---------- | -------- | -------- | ------- | ------------------- | ------------------- |
| program 1 | 01/01/2018 | 00:00:00 | 00:01:00 | track 1 | 01/01/2018 00:00:58 | 01/01/2018 00:01:58 |
| program 2 | 01/01/2018 | 00:01:00 | 00:02:00 | track 1 | 01/01/2018 00:00:58 | 01/01/2018 00:01:58 |
| program 3 | 01/01/2018 | 00:02:00 | 00:03:00 | track 2 | 01/01/2018 00:02:20 | 01/01/2018 00:02:40 |

| program   | date       | time     | duration | title   | start time          | end time            |
| --------- | ---------- | -------- | -------- | ------- | ------------------- | ------------------- |
| program 1 | 01/01/2018 | 00:00:00 | 00:01:00 |         |                     |                     |
| program 2 | 01/01/2018 | 00:01:00 | 00:02:00 | track 1 | 01/01/2018 00:01:00 | 01/01/2018 00:01:58 |
| program 3 | 01/01/2018 | 00:02:00 | 00:03:00 | track 2 | 01/01/2018 00:02:20 | 01/01/2018 00:02:40 |

### Enrich with external web API

The customer needs to have the spotify ids of the tracks in order to be able to pay the corresponding royalties to the owners. For this you should search each track in the [Spotify API](https://developer.spotify.com/documentation/web-api/), fins its spotify id if possible and add a column in the report with it. You can make use of the [spotipy python module](https://spotipy.readthedocs.io/en/latest/). 

## Deliverable
You are asked to provide a compressed file containing the resulting file in .csv format and the Python code you used to create the file. You should make the code as much modular and reusable as possible, good coding practices will be appreciated. 
