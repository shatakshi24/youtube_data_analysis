# youtube_data_analysis
Analysis of Youtube data in hdfs using pig tool

Step 1:upload the youtube datasets
hdfs dfs -copyFromLocal /home/edureka/youtubedata.txt /project
Problem Statement 1 :
Find out the top 5 categories with maximum number of videos uploaded.
[edureka@localhost ~]$ pig
grunt> A = LOAD '/project' AS (id:chararray, uploader:chararray, interval:int, category:chararray, length:int, noofviews:int, rating:float, noofratings:int, noofcomments:int, relatedvideos:chararray);
grunt> B = foreach A generate id, category;
grunt> C = group B by category;
D = foreach C generate group, COUNT(B) AS cnt;
grunt> E = ORDER D by cnt DESC;
grunt> F = LIMIT E 5;
STORE F INTO 'OUTPUT1';

Problem statement 2:
Find out the top 10 rated videos.
[edureka@localhost ~]$ pig
grunt> A = LOAD '/project' AS (id:chararray, uploader:chararray, interval:int,
category:chararray, length:int, noofviews:int, rating:float, noofratings:int,
noofcomments:int, relatedvideos:chararray);
grunt> B = foreach A generate id, rating;
grunt> C = ORDER B by rating DESC;
grunt> D = LIMIT C 5;
STORE D INTO 'OUTPUT2';

Problem Statement 3:
Find out the most viewed videos.
[edureka@localhost ~]$ pig
grunt> A = LOAD '/project' AS (id:chararray, uploader:chararray, interval:int, category:chararray, length:int, noofviews:int, rating:float, noofratings:int, noofcomments:int, relatedvideos:chararray);
grunt> B = foreach A generate id, noofviews;
grunt> C = ORDER B by rating DESC;
STORE C INTO 'OUTPUT3’;
