# Big_Data_ITMO


## Notebook "Prediction.ipynb"

This notebook is used to work with distributed storage files on a cluster. Namely, the prices of the cryptocurrency predicted by the model are read from HDFS, for which a comparative chart is then built.
To do this, first of all, a PySpark session is configured. The following are functions for searching and extracting information from required files in HDFS. And finally, a comparative graph is constructed.


## Notebook "PySpark_Tasks.ipynb"


The dataset located in HDFS contains data of ITMO community from vk.com (https://vk.com/club94). There are group posts, likes for these posts, followers, posts of followers from 2019, and users likes. For each task a solution that processes data using PySpark dataframes, pyspark built-in functions other functions was provided.

### Data:
- posts_api.json – Posts of ITMO community
- posts_likes.parquet – Likes for posts of ITMO community
- followers.parquet – users who follow ITMO community in vk.com
- followers_info.json – public info about followers of ITMO community
- followers_posts_api_final.json – public posts of the followers from their pages in vk.com 
- followers_posts_likes.parquet – likes for the public posts of the followers

### Tasks:
1) Find the top 20 posts in the group: (a) by likes; (b) by comments; (c) by reposts. 

2) Find the top 20 users by (a) likes and (b) reposts they have made (to trace reposts use "copy_history" field) 

3) Get reposts of the original posts of the itmo group (posts.json) from user posts (the result should be similar to (group_post_id, Array (user_post_ids)))

4) Build a dictionary that maps an emoticon to its corresponding sentiment. There should be three types of sentiment: negative, positive, neutral. For example:
{
   ":)": "positive",
   ":(": "negative",
    "=D": "positive",
    ":-|" : "neutral"
} 

UTF-based representation is also ok. The dictionay should contain 30-50 different emoticons of three mentioned above sentiments. For each emoticon (no matter what sentiment they represent) calculate: its overall count; frequency (number of posts they can be found in divided by total count of posts); average count per post (For instance, '=)' can appear multiple times in the same post, like 0-5.). Save all results to HDFS. Additionally, for each group print: top 10 most popular emoticons by their overall count; top 5 emoticons which have the greatest difference between their overall count and frequency; top 5 emoticons with average count per post.

   Requirement: 
   - use a dictionary of emoticons to look for them in texts
   - broadcast the dictionary
   - implement an UDF to process texts with dictionary of emoticons;
\n

5) Find probable “fans”. For each user find the top 10 other users whose posts this user likes. 

6) Find probable friends. If two users like each other posts they may be friends. Find pairs of users where both users are top likers of each other.

Bonus task:

7) Set spark.sql.autoBroadcastJoinThreshold to no more than 100 KB or even zero and apply bucketing to avoid SortMerge joins whenever it is possible. Make screenshots proving that there is no shuffle during join execution.
