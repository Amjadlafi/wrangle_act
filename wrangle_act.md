## Project: Wrangling and Analyze Data

## by Amjad Almutairi

# Introduction


 In this project 4 I am tryiing to wrangle WeRateDogs Twitter data, passing by the processes of data wrangling and then create a clear visualization , Using Python and its libraries

## Data Gathering
In the cell below, gather **all** three pieces of data for this project and load them in the notebook. **Note:** the methods required to gather each data are different.
1. Directly download the WeRateDogs Twitter archive data (twitter_archive_enhanced.csv)


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import requests
import json
import seaborn as sns
#import tweepy
%matplotlib inline
```


```python
#Twitter Archive Enhanced "TAE"
tweet_df = pd.read_csv('twitter-archive-enhanced.csv')
tweet_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>in_reply_to_status_id</th>
      <th>in_reply_to_user_id</th>
      <th>timestamp</th>
      <th>source</th>
      <th>text</th>
      <th>retweeted_status_id</th>
      <th>retweeted_status_user_id</th>
      <th>retweeted_status_timestamp</th>
      <th>expanded_urls</th>
      <th>rating_numerator</th>
      <th>rating_denominator</th>
      <th>name</th>
      <th>doggo</th>
      <th>floofer</th>
      <th>pupper</th>
      <th>puppo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>892420643555336193</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-08-01 16:23:56 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Phineas. He's a mystical boy. Only eve...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/892420643...</td>
      <td>13</td>
      <td>10</td>
      <td>Phineas</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>892177421306343426</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-08-01 00:17:27 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Tilly. She's just checking pup on you....</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/892177421...</td>
      <td>13</td>
      <td>10</td>
      <td>Tilly</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2</th>
      <td>891815181378084864</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-07-31 00:18:03 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Archie. He is a rare Norwegian Pouncin...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/891815181...</td>
      <td>12</td>
      <td>10</td>
      <td>Archie</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>891689557279858688</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-07-30 15:58:51 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Darla. She commenced a snooze mid meal...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/891689557...</td>
      <td>13</td>
      <td>10</td>
      <td>Darla</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>4</th>
      <td>891327558926688256</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-07-29 16:00:24 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Franklin. He would like you to stop ca...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/891327558...</td>
      <td>12</td>
      <td>10</td>
      <td>Franklin</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
</div>




```python
tweet_df[tweet_df.doggo != 'None']
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>in_reply_to_status_id</th>
      <th>in_reply_to_user_id</th>
      <th>timestamp</th>
      <th>source</th>
      <th>text</th>
      <th>retweeted_status_id</th>
      <th>retweeted_status_user_id</th>
      <th>retweeted_status_timestamp</th>
      <th>expanded_urls</th>
      <th>rating_numerator</th>
      <th>rating_denominator</th>
      <th>name</th>
      <th>doggo</th>
      <th>floofer</th>
      <th>pupper</th>
      <th>puppo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9</th>
      <td>890240255349198849</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-07-26 15:59:51 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Cassie. She is a college pup. Studying...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/890240255...</td>
      <td>14</td>
      <td>10</td>
      <td>Cassie</td>
      <td>doggo</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>43</th>
      <td>884162670584377345</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-07-09 21:29:42 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Meet Yogi. He doesn't have any important dog m...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/884162670...</td>
      <td>12</td>
      <td>10</td>
      <td>Yogi</td>
      <td>doggo</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>99</th>
      <td>872967104147763200</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-06-09 00:02:31 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here's a very large dog. He has a date later. ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/872967104...</td>
      <td>12</td>
      <td>10</td>
      <td>None</td>
      <td>doggo</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>108</th>
      <td>871515927908634625</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-06-04 23:56:03 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Napolean. He's a Raggedy East Nicaragu...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/871515927...</td>
      <td>12</td>
      <td>10</td>
      <td>Napolean</td>
      <td>doggo</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>110</th>
      <td>871102520638267392</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-06-03 20:33:19 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Never doubt a doggo 14/10 https://t.co/AbBLh2FZCH</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/animalcog/status/871075758...</td>
      <td>14</td>
      <td>10</td>
      <td>None</td>
      <td>doggo</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1117</th>
      <td>732375214819057664</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-05-17 01:00:32 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Kyle (pronounced 'Mitch'). He strives ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/732375214...</td>
      <td>11</td>
      <td>10</td>
      <td>Kyle</td>
      <td>doggo</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1141</th>
      <td>727644517743104000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-05-03 23:42:26 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here's a doggo struggling to cope with the win...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/727644517...</td>
      <td>13</td>
      <td>10</td>
      <td>None</td>
      <td>doggo</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1156</th>
      <td>724771698126512129</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-04-26 01:26:53 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Nothin better than a doggo and a sunset. 11/10...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/724771698...</td>
      <td>11</td>
      <td>10</td>
      <td>None</td>
      <td>doggo</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1176</th>
      <td>719991154352222208</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-04-12 20:50:42 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This doggo was initially thrilled when she saw...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/719991154...</td>
      <td>10</td>
      <td>10</td>
      <td>None</td>
      <td>doggo</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1204</th>
      <td>716080869887381504</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2016-04-02 01:52:38 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here's a super majestic doggo and a sunset 11/...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/716080869...</td>
      <td>11</td>
      <td>10</td>
      <td>None</td>
      <td>doggo</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
<p>97 rows × 17 columns</p>
</div>



2. Use the Requests library to download the tweet image prediction (image_predictions.tsv)


```python
url = ' https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv'
response = requests.get(url)

with open(url.split('/')[-1], mode = 'wb') as outfile:
    outfile.write(response.content)
image_df = pd.read_csv('image-predictions.tsv', sep = '\t', encoding = 'utf-8')
```


```python
image_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>jpg_url</th>
      <th>img_num</th>
      <th>p1</th>
      <th>p1_conf</th>
      <th>p1_dog</th>
      <th>p2</th>
      <th>p2_conf</th>
      <th>p2_dog</th>
      <th>p3</th>
      <th>p3_conf</th>
      <th>p3_dog</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>666020888022790149</td>
      <td>https://pbs.twimg.com/media/CT4udn0WwAA0aMy.jpg</td>
      <td>1</td>
      <td>Welsh_springer_spaniel</td>
      <td>0.465074</td>
      <td>True</td>
      <td>collie</td>
      <td>0.156665</td>
      <td>True</td>
      <td>Shetland_sheepdog</td>
      <td>0.061428</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>666029285002620928</td>
      <td>https://pbs.twimg.com/media/CT42GRgUYAA5iDo.jpg</td>
      <td>1</td>
      <td>redbone</td>
      <td>0.506826</td>
      <td>True</td>
      <td>miniature_pinscher</td>
      <td>0.074192</td>
      <td>True</td>
      <td>Rhodesian_ridgeback</td>
      <td>0.072010</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>666033412701032449</td>
      <td>https://pbs.twimg.com/media/CT4521TWwAEvMyu.jpg</td>
      <td>1</td>
      <td>German_shepherd</td>
      <td>0.596461</td>
      <td>True</td>
      <td>malinois</td>
      <td>0.138584</td>
      <td>True</td>
      <td>bloodhound</td>
      <td>0.116197</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>666044226329800704</td>
      <td>https://pbs.twimg.com/media/CT5Dr8HUEAA-lEu.jpg</td>
      <td>1</td>
      <td>Rhodesian_ridgeback</td>
      <td>0.408143</td>
      <td>True</td>
      <td>redbone</td>
      <td>0.360687</td>
      <td>True</td>
      <td>miniature_pinscher</td>
      <td>0.222752</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>666049248165822465</td>
      <td>https://pbs.twimg.com/media/CT5IQmsXIAAKY4A.jpg</td>
      <td>1</td>
      <td>miniature_pinscher</td>
      <td>0.560311</td>
      <td>True</td>
      <td>Rottweiler</td>
      <td>0.243682</td>
      <td>True</td>
      <td>Doberman</td>
      <td>0.154629</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



3. Use the Tweepy library to query additional data via the Twitter API (tweet_json.txt)

#### NOTE: `This is the calling Twitter API Code , but as I don't have twitter Developer Account I can't use it. So i downloaded the .json file directly.`


```python
# import tweepy
# from tweepy import OAuthHandler
# import json
# from timeit import default_timer as timer

# # Query Twitter API for each tweet in the Twitter archive and save JSON in a text file
# # These are hidden to comply with Twitter's API terms and conditions
# consumer_key = 'HIDDEN'
# consumer_secret = 'HIDDEN'
# access_token = 'HIDDEN'
# access_secret = 'HIDDEN'

# auth = OAuthHandler(consumer_key, consumer_secret)
# auth.set_access_token(access_token, access_secret)

# api = tweepy.API(auth, wait_on_rate_limit=True)

# # NOTE TO STUDENT WITH MOBILE VERIFICATION ISSUES:
# # df_1 is a DataFrame with the twitter_archive_enhanced.csv file. You may have to
# # change line 17 to match the name of your DataFrame with twitter_archive_enhanced.csv
# # NOTE TO REVIEWER: this student had mobile verification issues so the following
# # Twitter API code was sent to this student from a Udacity instructor
# # Tweet IDs for which to gather additional data via Twitter's API
# tweet_ids = df_1.tweet_id.values
# len(tweet_ids)

# # Query Twitter's API for JSON data for each tweet ID in the Twitter archive
# count = 0
# fails_dict = {}
# start = timer()
# # Save each tweet's returned JSON as a new line in a .txt file
# with open('tweet_json.txt', 'w') as outfile:
#     # This loop will likely take 20-30 minutes to run because of Twitter's rate limit
#     for tweet_id in tweet_ids:
#         count += 1
#         print(str(count) + ": " + str(tweet_id))
#         try:
#             tweet = api.get_status(tweet_id, tweet_mode='extended')
#             print("Success")
#             json.dump(tweet._json, outfile)
#             outfile.write('\n')
#         except tweepy.TweepError as e:
#             print("Fail")
#             fails_dict[tweet_id] = e
#             pass
# end = timer()
# print(end - start)
# print(fails_dict)
```


```python
df_json = pd.read_json('tweet-json.txt', lines=True)
df_json.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>created_at</th>
      <th>id</th>
      <th>id_str</th>
      <th>full_text</th>
      <th>truncated</th>
      <th>display_text_range</th>
      <th>entities</th>
      <th>extended_entities</th>
      <th>source</th>
      <th>in_reply_to_status_id</th>
      <th>...</th>
      <th>favorite_count</th>
      <th>favorited</th>
      <th>retweeted</th>
      <th>possibly_sensitive</th>
      <th>possibly_sensitive_appealable</th>
      <th>lang</th>
      <th>retweeted_status</th>
      <th>quoted_status_id</th>
      <th>quoted_status_id_str</th>
      <th>quoted_status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-08-01 16:23:56+00:00</td>
      <td>892420643555336193</td>
      <td>892420643555336192</td>
      <td>This is Phineas. He's a mystical boy. Only eve...</td>
      <td>False</td>
      <td>[0, 85]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 892420639486877696, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>39467</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-08-01 00:17:27+00:00</td>
      <td>892177421306343426</td>
      <td>892177421306343424</td>
      <td>This is Tilly. She's just checking pup on you....</td>
      <td>False</td>
      <td>[0, 138]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 892177413194625024, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>33819</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-07-31 00:18:03+00:00</td>
      <td>891815181378084864</td>
      <td>891815181378084864</td>
      <td>This is Archie. He is a rare Norwegian Pouncin...</td>
      <td>False</td>
      <td>[0, 121]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 891815175371796480, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>25461</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017-07-30 15:58:51+00:00</td>
      <td>891689557279858688</td>
      <td>891689557279858688</td>
      <td>This is Darla. She commenced a snooze mid meal...</td>
      <td>False</td>
      <td>[0, 79]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 891689552724799489, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>42908</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-07-29 16:00:24+00:00</td>
      <td>891327558926688256</td>
      <td>891327558926688256</td>
      <td>This is Franklin. He would like you to stop ca...</td>
      <td>False</td>
      <td>[0, 138]</td>
      <td>{'hashtags': [{'text': 'BarkWeek', 'indices': ...</td>
      <td>{'media': [{'id': 891327551943041024, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>41048</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 31 columns</p>
</div>






## Assessing Data
In this section, detect and document at least **eight (8) quality issues and two (2) tidiness issue**. You must use **both** visual assessment
programmatic assessement to assess the data.

**Note:** pay attention to the following key points when you access the data.

* You only want original ratings (no retweets) that have images. Though there are 5000+ tweets in the dataset, not all are dog ratings and some are retweets.
* Assessing and cleaning the entire dataset completely would require a lot of time, and is not necessary to practice and demonstrate your skills in data wrangling. Therefore, the requirements of this project are only to assess and clean at least 8 quality issues and at least 2 tidiness issues in this dataset.
* The fact that the rating numerators are greater than the denominators does not need to be cleaned. This [unique rating system](http://knowyourmeme.com/memes/theyre-good-dogs-brent) is a big part of the popularity of WeRateDogs.
* You do not need to gather the tweets beyond August 1st, 2017. You can, but note that you won't be able to gather the image predictions for these tweets since you don't have access to the algorithm used.


```python
df_json = df_json.rename(columns = {'id':'tweet_id'})
```

### Visual assessment:



```python
tweet_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>in_reply_to_status_id</th>
      <th>in_reply_to_user_id</th>
      <th>timestamp</th>
      <th>source</th>
      <th>text</th>
      <th>retweeted_status_id</th>
      <th>retweeted_status_user_id</th>
      <th>retweeted_status_timestamp</th>
      <th>expanded_urls</th>
      <th>rating_numerator</th>
      <th>rating_denominator</th>
      <th>name</th>
      <th>doggo</th>
      <th>floofer</th>
      <th>pupper</th>
      <th>puppo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>892420643555336193</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-08-01 16:23:56 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Phineas. He's a mystical boy. Only eve...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/892420643...</td>
      <td>13</td>
      <td>10</td>
      <td>Phineas</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>892177421306343426</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-08-01 00:17:27 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Tilly. She's just checking pup on you....</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/892177421...</td>
      <td>13</td>
      <td>10</td>
      <td>Tilly</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2</th>
      <td>891815181378084864</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-07-31 00:18:03 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Archie. He is a rare Norwegian Pouncin...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/891815181...</td>
      <td>12</td>
      <td>10</td>
      <td>Archie</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>891689557279858688</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-07-30 15:58:51 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Darla. She commenced a snooze mid meal...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/891689557...</td>
      <td>13</td>
      <td>10</td>
      <td>Darla</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>4</th>
      <td>891327558926688256</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-07-29 16:00:24 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Franklin. He would like you to stop ca...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/891327558...</td>
      <td>12</td>
      <td>10</td>
      <td>Franklin</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2351</th>
      <td>666049248165822465</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-11-16 00:24:50 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here we have a 1949 1st generation vulpix. Enj...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/666049248...</td>
      <td>5</td>
      <td>10</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2352</th>
      <td>666044226329800704</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-11-16 00:04:52 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is a purebred Piers Morgan. Loves to Netf...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/666044226...</td>
      <td>6</td>
      <td>10</td>
      <td>a</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2353</th>
      <td>666033412701032449</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-11-15 23:21:54 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here is a very happy pup. Big fan of well-main...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/666033412...</td>
      <td>9</td>
      <td>10</td>
      <td>a</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2354</th>
      <td>666029285002620928</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-11-15 23:05:30 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is a western brown Mitsubishi terrier. Up...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/666029285...</td>
      <td>7</td>
      <td>10</td>
      <td>a</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2355</th>
      <td>666020888022790149</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015-11-15 22:32:08 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here we have a Japanese Irish Setter. Lost eye...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/666020888...</td>
      <td>8</td>
      <td>10</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
<p>2356 rows × 17 columns</p>
</div>




```python
image_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>jpg_url</th>
      <th>img_num</th>
      <th>p1</th>
      <th>p1_conf</th>
      <th>p1_dog</th>
      <th>p2</th>
      <th>p2_conf</th>
      <th>p2_dog</th>
      <th>p3</th>
      <th>p3_conf</th>
      <th>p3_dog</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>666020888022790149</td>
      <td>https://pbs.twimg.com/media/CT4udn0WwAA0aMy.jpg</td>
      <td>1</td>
      <td>Welsh_springer_spaniel</td>
      <td>0.465074</td>
      <td>True</td>
      <td>collie</td>
      <td>0.156665</td>
      <td>True</td>
      <td>Shetland_sheepdog</td>
      <td>0.061428</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>666029285002620928</td>
      <td>https://pbs.twimg.com/media/CT42GRgUYAA5iDo.jpg</td>
      <td>1</td>
      <td>redbone</td>
      <td>0.506826</td>
      <td>True</td>
      <td>miniature_pinscher</td>
      <td>0.074192</td>
      <td>True</td>
      <td>Rhodesian_ridgeback</td>
      <td>0.072010</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>666033412701032449</td>
      <td>https://pbs.twimg.com/media/CT4521TWwAEvMyu.jpg</td>
      <td>1</td>
      <td>German_shepherd</td>
      <td>0.596461</td>
      <td>True</td>
      <td>malinois</td>
      <td>0.138584</td>
      <td>True</td>
      <td>bloodhound</td>
      <td>0.116197</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>666044226329800704</td>
      <td>https://pbs.twimg.com/media/CT5Dr8HUEAA-lEu.jpg</td>
      <td>1</td>
      <td>Rhodesian_ridgeback</td>
      <td>0.408143</td>
      <td>True</td>
      <td>redbone</td>
      <td>0.360687</td>
      <td>True</td>
      <td>miniature_pinscher</td>
      <td>0.222752</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>666049248165822465</td>
      <td>https://pbs.twimg.com/media/CT5IQmsXIAAKY4A.jpg</td>
      <td>1</td>
      <td>miniature_pinscher</td>
      <td>0.560311</td>
      <td>True</td>
      <td>Rottweiler</td>
      <td>0.243682</td>
      <td>True</td>
      <td>Doberman</td>
      <td>0.154629</td>
      <td>True</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2070</th>
      <td>891327558926688256</td>
      <td>https://pbs.twimg.com/media/DF6hr6BUMAAzZgT.jpg</td>
      <td>2</td>
      <td>basset</td>
      <td>0.555712</td>
      <td>True</td>
      <td>English_springer</td>
      <td>0.225770</td>
      <td>True</td>
      <td>German_short-haired_pointer</td>
      <td>0.175219</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2071</th>
      <td>891689557279858688</td>
      <td>https://pbs.twimg.com/media/DF_q7IAWsAEuuN8.jpg</td>
      <td>1</td>
      <td>paper_towel</td>
      <td>0.170278</td>
      <td>False</td>
      <td>Labrador_retriever</td>
      <td>0.168086</td>
      <td>True</td>
      <td>spatula</td>
      <td>0.040836</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2072</th>
      <td>891815181378084864</td>
      <td>https://pbs.twimg.com/media/DGBdLU1WsAANxJ9.jpg</td>
      <td>1</td>
      <td>Chihuahua</td>
      <td>0.716012</td>
      <td>True</td>
      <td>malamute</td>
      <td>0.078253</td>
      <td>True</td>
      <td>kelpie</td>
      <td>0.031379</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2073</th>
      <td>892177421306343426</td>
      <td>https://pbs.twimg.com/media/DGGmoV4XsAAUL6n.jpg</td>
      <td>1</td>
      <td>Chihuahua</td>
      <td>0.323581</td>
      <td>True</td>
      <td>Pekinese</td>
      <td>0.090647</td>
      <td>True</td>
      <td>papillon</td>
      <td>0.068957</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2074</th>
      <td>892420643555336193</td>
      <td>https://pbs.twimg.com/media/DGKD1-bXoAAIAUK.jpg</td>
      <td>1</td>
      <td>orange</td>
      <td>0.097049</td>
      <td>False</td>
      <td>bagel</td>
      <td>0.085851</td>
      <td>False</td>
      <td>banana</td>
      <td>0.076110</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
<p>2075 rows × 12 columns</p>
</div>




```python
df_json
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>created_at</th>
      <th>tweet_id</th>
      <th>id_str</th>
      <th>full_text</th>
      <th>truncated</th>
      <th>display_text_range</th>
      <th>entities</th>
      <th>extended_entities</th>
      <th>source</th>
      <th>in_reply_to_status_id</th>
      <th>...</th>
      <th>favorite_count</th>
      <th>favorited</th>
      <th>retweeted</th>
      <th>possibly_sensitive</th>
      <th>possibly_sensitive_appealable</th>
      <th>lang</th>
      <th>retweeted_status</th>
      <th>quoted_status_id</th>
      <th>quoted_status_id_str</th>
      <th>quoted_status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-08-01 16:23:56+00:00</td>
      <td>892420643555336193</td>
      <td>892420643555336192</td>
      <td>This is Phineas. He's a mystical boy. Only eve...</td>
      <td>False</td>
      <td>[0, 85]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 892420639486877696, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>39467</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-08-01 00:17:27+00:00</td>
      <td>892177421306343426</td>
      <td>892177421306343424</td>
      <td>This is Tilly. She's just checking pup on you....</td>
      <td>False</td>
      <td>[0, 138]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 892177413194625024, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>33819</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-07-31 00:18:03+00:00</td>
      <td>891815181378084864</td>
      <td>891815181378084864</td>
      <td>This is Archie. He is a rare Norwegian Pouncin...</td>
      <td>False</td>
      <td>[0, 121]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 891815175371796480, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>25461</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017-07-30 15:58:51+00:00</td>
      <td>891689557279858688</td>
      <td>891689557279858688</td>
      <td>This is Darla. She commenced a snooze mid meal...</td>
      <td>False</td>
      <td>[0, 79]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 891689552724799489, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>42908</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-07-29 16:00:24+00:00</td>
      <td>891327558926688256</td>
      <td>891327558926688256</td>
      <td>This is Franklin. He would like you to stop ca...</td>
      <td>False</td>
      <td>[0, 138]</td>
      <td>{'hashtags': [{'text': 'BarkWeek', 'indices': ...</td>
      <td>{'media': [{'id': 891327551943041024, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>41048</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2349</th>
      <td>2015-11-16 00:24:50+00:00</td>
      <td>666049248165822465</td>
      <td>666049248165822464</td>
      <td>Here we have a 1949 1st generation vulpix. Enj...</td>
      <td>False</td>
      <td>[0, 120]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 666049244999131136, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>111</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2350</th>
      <td>2015-11-16 00:04:52+00:00</td>
      <td>666044226329800704</td>
      <td>666044226329800704</td>
      <td>This is a purebred Piers Morgan. Loves to Netf...</td>
      <td>False</td>
      <td>[0, 137]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 666044217047650304, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>311</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2351</th>
      <td>2015-11-15 23:21:54+00:00</td>
      <td>666033412701032449</td>
      <td>666033412701032448</td>
      <td>Here is a very happy pup. Big fan of well-main...</td>
      <td>False</td>
      <td>[0, 130]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 666033409081393153, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>128</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2352</th>
      <td>2015-11-15 23:05:30+00:00</td>
      <td>666029285002620928</td>
      <td>666029285002620928</td>
      <td>This is a western brown Mitsubishi terrier. Up...</td>
      <td>False</td>
      <td>[0, 139]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 666029276303482880, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>132</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2353</th>
      <td>2015-11-15 22:32:08+00:00</td>
      <td>666020888022790149</td>
      <td>666020888022790144</td>
      <td>Here we have a Japanese Irish Setter. Lost eye...</td>
      <td>False</td>
      <td>[0, 131]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 666020881337073664, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>2535</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>2354 rows × 31 columns</p>
</div>



### Programmatic assessment:



```python
tweet_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2356 entries, 0 to 2355
    Data columns (total 17 columns):
     #   Column                      Non-Null Count  Dtype  
    ---  ------                      --------------  -----  
     0   tweet_id                    2356 non-null   int64  
     1   in_reply_to_status_id       78 non-null     float64
     2   in_reply_to_user_id         78 non-null     float64
     3   timestamp                   2356 non-null   object 
     4   source                      2356 non-null   object 
     5   text                        2356 non-null   object 
     6   retweeted_status_id         181 non-null    float64
     7   retweeted_status_user_id    181 non-null    float64
     8   retweeted_status_timestamp  181 non-null    object 
     9   expanded_urls               2297 non-null   object 
     10  rating_numerator            2356 non-null   int64  
     11  rating_denominator          2356 non-null   int64  
     12  name                        2356 non-null   object 
     13  doggo                       2356 non-null   object 
     14  floofer                     2356 non-null   object 
     15  pupper                      2356 non-null   object 
     16  puppo                       2356 non-null   object 
    dtypes: float64(4), int64(3), object(10)
    memory usage: 313.0+ KB
    


```python
tweet_df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>in_reply_to_status_id</th>
      <th>in_reply_to_user_id</th>
      <th>retweeted_status_id</th>
      <th>retweeted_status_user_id</th>
      <th>rating_numerator</th>
      <th>rating_denominator</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>2.356000e+03</td>
      <td>7.800000e+01</td>
      <td>7.800000e+01</td>
      <td>1.810000e+02</td>
      <td>1.810000e+02</td>
      <td>2356.000000</td>
      <td>2356.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>7.427716e+17</td>
      <td>7.455079e+17</td>
      <td>2.014171e+16</td>
      <td>7.720400e+17</td>
      <td>1.241698e+16</td>
      <td>13.126486</td>
      <td>10.455433</td>
    </tr>
    <tr>
      <th>std</th>
      <td>6.856705e+16</td>
      <td>7.582492e+16</td>
      <td>1.252797e+17</td>
      <td>6.236928e+16</td>
      <td>9.599254e+16</td>
      <td>45.876648</td>
      <td>6.745237</td>
    </tr>
    <tr>
      <th>min</th>
      <td>6.660209e+17</td>
      <td>6.658147e+17</td>
      <td>1.185634e+07</td>
      <td>6.661041e+17</td>
      <td>7.832140e+05</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.783989e+17</td>
      <td>6.757419e+17</td>
      <td>3.086374e+08</td>
      <td>7.186315e+17</td>
      <td>4.196984e+09</td>
      <td>10.000000</td>
      <td>10.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>7.196279e+17</td>
      <td>7.038708e+17</td>
      <td>4.196984e+09</td>
      <td>7.804657e+17</td>
      <td>4.196984e+09</td>
      <td>11.000000</td>
      <td>10.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>7.993373e+17</td>
      <td>8.257804e+17</td>
      <td>4.196984e+09</td>
      <td>8.203146e+17</td>
      <td>4.196984e+09</td>
      <td>12.000000</td>
      <td>10.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>8.924206e+17</td>
      <td>8.862664e+17</td>
      <td>8.405479e+17</td>
      <td>8.874740e+17</td>
      <td>7.874618e+17</td>
      <td>1776.000000</td>
      <td>170.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
sum(tweet_df.tweet_id.isnull())

```




    0




```python
sum(tweet_df.tweet_id.duplicated())

```




    0




```python
tweet_df.rating_numerator.value_counts()

```




    12      558
    11      464
    10      461
    13      351
    9       158
    8       102
    7        55
    14       54
    5        37
    6        32
    3        19
    4        17
    1         9
    2         9
    0         2
    15        2
    75        2
    420       2
    182       1
    204       1
    143       1
    121       1
    99        1
    20        1
    45        1
    27        1
    17        1
    24        1
    26        1
    44        1
    50        1
    60        1
    80        1
    84        1
    88        1
    1776      1
    960       1
    666       1
    144       1
    165       1
    Name: rating_numerator, dtype: int64




```python
tweet_df.name.value_counts().head()

```




    None       745
    a           55
    Charlie     12
    Cooper      11
    Oliver      11
    Name: name, dtype: int64



### tweet image prediction



```python
image_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2075 entries, 0 to 2074
    Data columns (total 12 columns):
     #   Column    Non-Null Count  Dtype  
    ---  ------    --------------  -----  
     0   tweet_id  2075 non-null   int64  
     1   jpg_url   2075 non-null   object 
     2   img_num   2075 non-null   int64  
     3   p1        2075 non-null   object 
     4   p1_conf   2075 non-null   float64
     5   p1_dog    2075 non-null   bool   
     6   p2        2075 non-null   object 
     7   p2_conf   2075 non-null   float64
     8   p2_dog    2075 non-null   bool   
     9   p3        2075 non-null   object 
     10  p3_conf   2075 non-null   float64
     11  p3_dog    2075 non-null   bool   
    dtypes: bool(3), float64(3), int64(2), object(4)
    memory usage: 152.1+ KB
    


```python
image_df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>img_num</th>
      <th>p1_conf</th>
      <th>p2_conf</th>
      <th>p3_conf</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>2.075000e+03</td>
      <td>2075.000000</td>
      <td>2075.000000</td>
      <td>2.075000e+03</td>
      <td>2.075000e+03</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>7.384514e+17</td>
      <td>1.203855</td>
      <td>0.594548</td>
      <td>1.345886e-01</td>
      <td>6.032417e-02</td>
    </tr>
    <tr>
      <th>std</th>
      <td>6.785203e+16</td>
      <td>0.561875</td>
      <td>0.271174</td>
      <td>1.006657e-01</td>
      <td>5.090593e-02</td>
    </tr>
    <tr>
      <th>min</th>
      <td>6.660209e+17</td>
      <td>1.000000</td>
      <td>0.044333</td>
      <td>1.011300e-08</td>
      <td>1.740170e-10</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.764835e+17</td>
      <td>1.000000</td>
      <td>0.364412</td>
      <td>5.388625e-02</td>
      <td>1.622240e-02</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>7.119988e+17</td>
      <td>1.000000</td>
      <td>0.588230</td>
      <td>1.181810e-01</td>
      <td>4.944380e-02</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>7.932034e+17</td>
      <td>1.000000</td>
      <td>0.843855</td>
      <td>1.955655e-01</td>
      <td>9.180755e-02</td>
    </tr>
    <tr>
      <th>max</th>
      <td>8.924206e+17</td>
      <td>4.000000</td>
      <td>1.000000</td>
      <td>4.880140e-01</td>
      <td>2.734190e-01</td>
    </tr>
  </tbody>
</table>
</div>




```python
sum(image_df.duplicated())

```




    0




```python
image_df.img_num.value_counts()

```




    1    1780
    2     198
    3      66
    4      31
    Name: img_num, dtype: int64




```python
image_df.p1.value_counts()

```




    golden_retriever      150
    Labrador_retriever    100
    Pembroke               89
    Chihuahua              83
    pug                    57
                         ... 
    cup                     1
    standard_schnauzer      1
    grey_fox                1
    hare                    1
    teapot                  1
    Name: p1, Length: 378, dtype: int64




```python
image_df.p2.value_counts()

```




    Labrador_retriever    104
    golden_retriever       92
    Cardigan               73
    Chihuahua              44
    Pomeranian             42
                         ... 
    knee_pad                1
    lampshade               1
    streetcar               1
    mosquito_net            1
    barbershop              1
    Name: p2, Length: 405, dtype: int64




```python
image_df.p3.value_counts()

```




    Labrador_retriever    79
    Chihuahua             58
    golden_retriever      48
    Eskimo_dog            38
    kelpie                35
                          ..
    crayfish               1
    mushroom               1
    axolotl                1
    cloak                  1
    wombat                 1
    Name: p3, Length: 408, dtype: int64



## Twitter API

 Each tweet's retweet count and favorite ("like") count at minimum, and any additional data you find interesting. Using the tweet IDs in the WeRateDogs Twitter archive, I query the Twitter API for each tweet's JSON data using Python's Tweepy library and store each tweet's entire set of JSON data in a file called tweet_json.txt file. Each tweet's JSON data written to its own line. Then I read this .txt file line by line into a pandas DataFrame .


```python
df_json.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2354 entries, 0 to 2353
    Data columns (total 31 columns):
     #   Column                         Non-Null Count  Dtype              
    ---  ------                         --------------  -----              
     0   created_at                     2354 non-null   datetime64[ns, UTC]
     1   tweet_id                       2354 non-null   int64              
     2   id_str                         2354 non-null   int64              
     3   full_text                      2354 non-null   object             
     4   truncated                      2354 non-null   bool               
     5   display_text_range             2354 non-null   object             
     6   entities                       2354 non-null   object             
     7   extended_entities              2073 non-null   object             
     8   source                         2354 non-null   object             
     9   in_reply_to_status_id          78 non-null     float64            
     10  in_reply_to_status_id_str      78 non-null     float64            
     11  in_reply_to_user_id            78 non-null     float64            
     12  in_reply_to_user_id_str        78 non-null     float64            
     13  in_reply_to_screen_name        78 non-null     object             
     14  user                           2354 non-null   object             
     15  geo                            0 non-null      float64            
     16  coordinates                    0 non-null      float64            
     17  place                          1 non-null      object             
     18  contributors                   0 non-null      float64            
     19  is_quote_status                2354 non-null   bool               
     20  retweet_count                  2354 non-null   int64              
     21  favorite_count                 2354 non-null   int64              
     22  favorited                      2354 non-null   bool               
     23  retweeted                      2354 non-null   bool               
     24  possibly_sensitive             2211 non-null   float64            
     25  possibly_sensitive_appealable  2211 non-null   float64            
     26  lang                           2354 non-null   object             
     27  retweeted_status               179 non-null    object             
     28  quoted_status_id               29 non-null     float64            
     29  quoted_status_id_str           29 non-null     float64            
     30  quoted_status                  28 non-null     object             
    dtypes: bool(4), datetime64[ns, UTC](1), float64(11), int64(4), object(11)
    memory usage: 505.9+ KB
    


```python
df_json.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>id_str</th>
      <th>in_reply_to_status_id</th>
      <th>in_reply_to_status_id_str</th>
      <th>in_reply_to_user_id</th>
      <th>in_reply_to_user_id_str</th>
      <th>geo</th>
      <th>coordinates</th>
      <th>contributors</th>
      <th>retweet_count</th>
      <th>favorite_count</th>
      <th>possibly_sensitive</th>
      <th>possibly_sensitive_appealable</th>
      <th>quoted_status_id</th>
      <th>quoted_status_id_str</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>2.354000e+03</td>
      <td>2.354000e+03</td>
      <td>7.800000e+01</td>
      <td>7.800000e+01</td>
      <td>7.800000e+01</td>
      <td>7.800000e+01</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2354.000000</td>
      <td>2354.000000</td>
      <td>2211.0</td>
      <td>2211.0</td>
      <td>2.900000e+01</td>
      <td>2.900000e+01</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>7.426978e+17</td>
      <td>7.426978e+17</td>
      <td>7.455079e+17</td>
      <td>7.455079e+17</td>
      <td>2.014171e+16</td>
      <td>2.014171e+16</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3164.797366</td>
      <td>8080.968564</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>8.162686e+17</td>
      <td>8.162686e+17</td>
    </tr>
    <tr>
      <th>std</th>
      <td>6.852812e+16</td>
      <td>6.852812e+16</td>
      <td>7.582492e+16</td>
      <td>7.582492e+16</td>
      <td>1.252797e+17</td>
      <td>1.252797e+17</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5284.770364</td>
      <td>11814.771334</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>6.164161e+16</td>
      <td>6.164161e+16</td>
    </tr>
    <tr>
      <th>min</th>
      <td>6.660209e+17</td>
      <td>6.660209e+17</td>
      <td>6.658147e+17</td>
      <td>6.658147e+17</td>
      <td>1.185634e+07</td>
      <td>1.185634e+07</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>6.721083e+17</td>
      <td>6.721083e+17</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.783975e+17</td>
      <td>6.783975e+17</td>
      <td>6.757419e+17</td>
      <td>6.757419e+17</td>
      <td>3.086374e+08</td>
      <td>3.086374e+08</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>624.500000</td>
      <td>1415.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>7.888183e+17</td>
      <td>7.888183e+17</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>7.194596e+17</td>
      <td>7.194596e+17</td>
      <td>7.038708e+17</td>
      <td>7.038708e+17</td>
      <td>4.196984e+09</td>
      <td>4.196984e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1473.500000</td>
      <td>3603.500000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>8.340867e+17</td>
      <td>8.340867e+17</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>7.993058e+17</td>
      <td>7.993058e+17</td>
      <td>8.257804e+17</td>
      <td>8.257804e+17</td>
      <td>4.196984e+09</td>
      <td>4.196984e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3652.000000</td>
      <td>10122.250000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>8.664587e+17</td>
      <td>8.664587e+17</td>
    </tr>
    <tr>
      <th>max</th>
      <td>8.924206e+17</td>
      <td>8.924206e+17</td>
      <td>8.862664e+17</td>
      <td>8.862664e+17</td>
      <td>8.405479e+17</td>
      <td>8.405479e+17</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>79515.000000</td>
      <td>132810.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>8.860534e+17</td>
      <td>8.860534e+17</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_json.isnull().sum()

```




    created_at                          0
    tweet_id                            0
    id_str                              0
    full_text                           0
    truncated                           0
    display_text_range                  0
    entities                            0
    extended_entities                 281
    source                              0
    in_reply_to_status_id            2276
    in_reply_to_status_id_str        2276
    in_reply_to_user_id              2276
    in_reply_to_user_id_str          2276
    in_reply_to_screen_name          2276
    user                                0
    geo                              2354
    coordinates                      2354
    place                            2353
    contributors                     2354
    is_quote_status                     0
    retweet_count                       0
    favorite_count                      0
    favorited                           0
    retweeted                           0
    possibly_sensitive                143
    possibly_sensitive_appealable     143
    lang                                0
    retweeted_status                 2175
    quoted_status_id                 2325
    quoted_status_id_str             2325
    quoted_status                    2326
    dtype: int64



### Quality issues

1.There are missing values in (in_reply_to_status_id, in_reply_to_user_id) columns and because these columns have many missings I will delete the whole columns. Then delete retweeted tweets

2.tweet_id is an integer which is a data type issue, we need to convert it to string.

3.The data in columns (p1, p2, and p3) had uppercase





4.Non-descriptive names of columns.



5.incorrect some of dogs name like (''one'', "a", "an", "by","very") ,replaced with no name

6.Change Timestamp datatype from Object/String to Datetime

7.Change Text range each tweet to be integer because it always starts from 0

8.rating's numerator and denominator should be calculated in one column then change the type to be float.

### Tidiness issues

1.Create one column for dog stags(doggo, floofer, pupper, puppo)


2.Merging all dataframes into one data frame




## Cleaning Data
In this section, clean **all** of the issues you documented while assessing. 

**Note:** Make a copy of the original data before cleaning. Cleaning includes merging individual pieces of data according to the rules of [tidy data](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html). The result should be a high-quality and tidy master pandas DataFrame (or DataFrames, if appropriate).


```python
# Make copies of original pieces of data
tweet_clean = tweet_df.copy()
image_clean = image_df.copy()
json_clean = df_json.copy()
```


```python
# tweet_clean['rating'] = tweet_clean['rating_numerator'].apply(lambda x : float(x)) / tweet_clean['rating_denominator'].apply(lambda x : float(x))
```


```python
tweet_clean.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2356 entries, 0 to 2355
    Data columns (total 17 columns):
     #   Column                      Non-Null Count  Dtype  
    ---  ------                      --------------  -----  
     0   tweet_id                    2356 non-null   int64  
     1   in_reply_to_status_id       78 non-null     float64
     2   in_reply_to_user_id         78 non-null     float64
     3   timestamp                   2356 non-null   object 
     4   source                      2356 non-null   object 
     5   text                        2356 non-null   object 
     6   retweeted_status_id         181 non-null    float64
     7   retweeted_status_user_id    181 non-null    float64
     8   retweeted_status_timestamp  181 non-null    object 
     9   expanded_urls               2297 non-null   object 
     10  rating_numerator            2356 non-null   int64  
     11  rating_denominator          2356 non-null   int64  
     12  name                        2356 non-null   object 
     13  doggo                       2356 non-null   object 
     14  floofer                     2356 non-null   object 
     15  pupper                      2356 non-null   object 
     16  puppo                       2356 non-null   object 
    dtypes: float64(4), int64(3), object(10)
    memory usage: 313.0+ KB
    


```python
tweet_clean.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2356 entries, 0 to 2355
    Data columns (total 17 columns):
     #   Column                      Non-Null Count  Dtype  
    ---  ------                      --------------  -----  
     0   tweet_id                    2356 non-null   int64  
     1   in_reply_to_status_id       78 non-null     float64
     2   in_reply_to_user_id         78 non-null     float64
     3   timestamp                   2356 non-null   object 
     4   source                      2356 non-null   object 
     5   text                        2356 non-null   object 
     6   retweeted_status_id         181 non-null    float64
     7   retweeted_status_user_id    181 non-null    float64
     8   retweeted_status_timestamp  181 non-null    object 
     9   expanded_urls               2297 non-null   object 
     10  rating_numerator            2356 non-null   int64  
     11  rating_denominator          2356 non-null   int64  
     12  name                        2356 non-null   object 
     13  doggo                       2356 non-null   object 
     14  floofer                     2356 non-null   object 
     15  pupper                      2356 non-null   object 
     16  puppo                       2356 non-null   object 
    dtypes: float64(4), int64(3), object(10)
    memory usage: 313.0+ KB
    

### 1 Issue : Missing values and Duplicated tweets ( retweeted tweets )

#### Define:

There are missing values in (in_reply_to_status_id, in_reply_to_user_id) columns and because these columns have many missings I will delete the whole columns. Then delete retweeted tweets


```python
tweet_clean.head(1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>in_reply_to_status_id</th>
      <th>in_reply_to_user_id</th>
      <th>timestamp</th>
      <th>source</th>
      <th>text</th>
      <th>retweeted_status_id</th>
      <th>retweeted_status_user_id</th>
      <th>retweeted_status_timestamp</th>
      <th>expanded_urls</th>
      <th>rating_numerator</th>
      <th>rating_denominator</th>
      <th>name</th>
      <th>doggo</th>
      <th>floofer</th>
      <th>pupper</th>
      <th>puppo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>892420643555336193</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017-08-01 16:23:56 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Phineas. He's a mystical boy. Only eve...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>https://twitter.com/dog_rates/status/892420643...</td>
      <td>13</td>
      <td>10</td>
      <td>Phineas</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
</div>



### code


```python
tweet_clean.drop(columns=['in_reply_to_status_id', 'in_reply_to_user_id'] , inplace=True)
```


```python
tweet_clean = tweet_clean[tweet_clean.retweeted_status_id.isnull() & tweet_clean.retweeted_status_user_id.isnull() & tweet_clean.retweeted_status_timestamp.isnull() ]
```


```python
tweet_clean.info()

```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 2175 entries, 0 to 2355
    Data columns (total 15 columns):
     #   Column                      Non-Null Count  Dtype  
    ---  ------                      --------------  -----  
     0   tweet_id                    2175 non-null   int64  
     1   timestamp                   2175 non-null   object 
     2   source                      2175 non-null   object 
     3   text                        2175 non-null   object 
     4   retweeted_status_id         0 non-null      float64
     5   retweeted_status_user_id    0 non-null      float64
     6   retweeted_status_timestamp  0 non-null      object 
     7   expanded_urls               2117 non-null   object 
     8   rating_numerator            2175 non-null   int64  
     9   rating_denominator          2175 non-null   int64  
     10  name                        2175 non-null   object 
     11  doggo                       2175 non-null   object 
     12  floofer                     2175 non-null   object 
     13  pupper                      2175 non-null   object 
     14  puppo                       2175 non-null   object 
    dtypes: float64(2), int64(3), object(10)
    memory usage: 271.9+ KB
    


```python
tweet_clean.drop(columns=['retweeted_status_id', 'retweeted_status_user_id' , 'retweeted_status_timestamp'] , inplace=True)
```


```python
tweet_clean.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 2175 entries, 0 to 2355
    Data columns (total 12 columns):
     #   Column              Non-Null Count  Dtype 
    ---  ------              --------------  ----- 
     0   tweet_id            2175 non-null   int64 
     1   timestamp           2175 non-null   object
     2   source              2175 non-null   object
     3   text                2175 non-null   object
     4   expanded_urls       2117 non-null   object
     5   rating_numerator    2175 non-null   int64 
     6   rating_denominator  2175 non-null   int64 
     7   name                2175 non-null   object
     8   doggo               2175 non-null   object
     9   floofer             2175 non-null   object
     10  pupper              2175 non-null   object
     11  puppo               2175 non-null   object
    dtypes: int64(3), object(9)
    memory usage: 220.9+ KB
    

#### Test


```python
tweet_clean
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>timestamp</th>
      <th>source</th>
      <th>text</th>
      <th>expanded_urls</th>
      <th>rating_numerator</th>
      <th>rating_denominator</th>
      <th>name</th>
      <th>doggo</th>
      <th>floofer</th>
      <th>pupper</th>
      <th>puppo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>892420643555336193</td>
      <td>2017-08-01 16:23:56 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Phineas. He's a mystical boy. Only eve...</td>
      <td>https://twitter.com/dog_rates/status/892420643...</td>
      <td>13</td>
      <td>10</td>
      <td>Phineas</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>892177421306343426</td>
      <td>2017-08-01 00:17:27 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Tilly. She's just checking pup on you....</td>
      <td>https://twitter.com/dog_rates/status/892177421...</td>
      <td>13</td>
      <td>10</td>
      <td>Tilly</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2</th>
      <td>891815181378084864</td>
      <td>2017-07-31 00:18:03 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Archie. He is a rare Norwegian Pouncin...</td>
      <td>https://twitter.com/dog_rates/status/891815181...</td>
      <td>12</td>
      <td>10</td>
      <td>Archie</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>891689557279858688</td>
      <td>2017-07-30 15:58:51 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Darla. She commenced a snooze mid meal...</td>
      <td>https://twitter.com/dog_rates/status/891689557...</td>
      <td>13</td>
      <td>10</td>
      <td>Darla</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>4</th>
      <td>891327558926688256</td>
      <td>2017-07-29 16:00:24 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Franklin. He would like you to stop ca...</td>
      <td>https://twitter.com/dog_rates/status/891327558...</td>
      <td>12</td>
      <td>10</td>
      <td>Franklin</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2351</th>
      <td>666049248165822465</td>
      <td>2015-11-16 00:24:50 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here we have a 1949 1st generation vulpix. Enj...</td>
      <td>https://twitter.com/dog_rates/status/666049248...</td>
      <td>5</td>
      <td>10</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2352</th>
      <td>666044226329800704</td>
      <td>2015-11-16 00:04:52 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is a purebred Piers Morgan. Loves to Netf...</td>
      <td>https://twitter.com/dog_rates/status/666044226...</td>
      <td>6</td>
      <td>10</td>
      <td>a</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2353</th>
      <td>666033412701032449</td>
      <td>2015-11-15 23:21:54 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here is a very happy pup. Big fan of well-main...</td>
      <td>https://twitter.com/dog_rates/status/666033412...</td>
      <td>9</td>
      <td>10</td>
      <td>a</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2354</th>
      <td>666029285002620928</td>
      <td>2015-11-15 23:05:30 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is a western brown Mitsubishi terrier. Up...</td>
      <td>https://twitter.com/dog_rates/status/666029285...</td>
      <td>7</td>
      <td>10</td>
      <td>a</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2355</th>
      <td>666020888022790149</td>
      <td>2015-11-15 22:32:08 +0000</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here we have a Japanese Irish Setter. Lost eye...</td>
      <td>https://twitter.com/dog_rates/status/666020888...</td>
      <td>8</td>
      <td>10</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
<p>2175 rows × 12 columns</p>
</div>



### 2 Issue : 

Incorrected datatype on tweet_id it int, and I will convert it to a string


## code:




```python
tweet_clean['tweet_id'] =tweet_clean['tweet_id'].astype(str)
```


```python
image_clean['tweet_id'] = tweet_clean['tweet_id'].astype(str)

```


```python
df_json = df_json.rename(columns = {'id':'tweet_id'})
```


```python
json_clean.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>created_at</th>
      <th>tweet_id</th>
      <th>id_str</th>
      <th>full_text</th>
      <th>truncated</th>
      <th>display_text_range</th>
      <th>entities</th>
      <th>extended_entities</th>
      <th>source</th>
      <th>in_reply_to_status_id</th>
      <th>...</th>
      <th>favorite_count</th>
      <th>favorited</th>
      <th>retweeted</th>
      <th>possibly_sensitive</th>
      <th>possibly_sensitive_appealable</th>
      <th>lang</th>
      <th>retweeted_status</th>
      <th>quoted_status_id</th>
      <th>quoted_status_id_str</th>
      <th>quoted_status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-08-01 16:23:56+00:00</td>
      <td>892420643555336193</td>
      <td>892420643555336192</td>
      <td>This is Phineas. He's a mystical boy. Only eve...</td>
      <td>False</td>
      <td>[0, 85]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 892420639486877696, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>39467</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-08-01 00:17:27+00:00</td>
      <td>892177421306343426</td>
      <td>892177421306343424</td>
      <td>This is Tilly. She's just checking pup on you....</td>
      <td>False</td>
      <td>[0, 138]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 892177413194625024, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>33819</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-07-31 00:18:03+00:00</td>
      <td>891815181378084864</td>
      <td>891815181378084864</td>
      <td>This is Archie. He is a rare Norwegian Pouncin...</td>
      <td>False</td>
      <td>[0, 121]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 891815175371796480, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>25461</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017-07-30 15:58:51+00:00</td>
      <td>891689557279858688</td>
      <td>891689557279858688</td>
      <td>This is Darla. She commenced a snooze mid meal...</td>
      <td>False</td>
      <td>[0, 79]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 891689552724799489, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>42908</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-07-29 16:00:24+00:00</td>
      <td>891327558926688256</td>
      <td>891327558926688256</td>
      <td>This is Franklin. He would like you to stop ca...</td>
      <td>False</td>
      <td>[0, 138]</td>
      <td>{'hashtags': [{'text': 'BarkWeek', 'indices': ...</td>
      <td>{'media': [{'id': 891327551943041024, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>41048</td>
      <td>False</td>
      <td>False</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>en</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 31 columns</p>
</div>




```python
tweet_clean['tweet_id'] = tweet_clean['tweet_id'].astype(str)

```

## Test


```python
tweet_clean.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 2175 entries, 0 to 2355
    Data columns (total 12 columns):
     #   Column              Non-Null Count  Dtype 
    ---  ------              --------------  ----- 
     0   tweet_id            2175 non-null   object
     1   timestamp           2175 non-null   object
     2   source              2175 non-null   object
     3   text                2175 non-null   object
     4   expanded_urls       2117 non-null   object
     5   rating_numerator    2175 non-null   int64 
     6   rating_denominator  2175 non-null   int64 
     7   name                2175 non-null   object
     8   doggo               2175 non-null   object
     9   floofer             2175 non-null   object
     10  pupper              2175 non-null   object
     11  puppo               2175 non-null   object
    dtypes: int64(2), object(10)
    memory usage: 285.4+ KB
    

### 3 Issue :

The data in columns (p1, p2, and p3) had uppercase





## Code


```python
image_clean['p1'] = image_clean['p1'].str.lower()
image_clean['p2'] = image_clean['p2'].str.lower()
image_clean['p3'] = image_clean['p3'].str.lower()
```

## TEST


```python
image_clean.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>jpg_url</th>
      <th>img_num</th>
      <th>p1</th>
      <th>p1_conf</th>
      <th>p1_dog</th>
      <th>p2</th>
      <th>p2_conf</th>
      <th>p2_dog</th>
      <th>p3</th>
      <th>p3_conf</th>
      <th>p3_dog</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>892420643555336193</td>
      <td>https://pbs.twimg.com/media/CT4udn0WwAA0aMy.jpg</td>
      <td>1</td>
      <td>welsh_springer_spaniel</td>
      <td>0.465074</td>
      <td>True</td>
      <td>collie</td>
      <td>0.156665</td>
      <td>True</td>
      <td>shetland_sheepdog</td>
      <td>0.061428</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>892177421306343426</td>
      <td>https://pbs.twimg.com/media/CT42GRgUYAA5iDo.jpg</td>
      <td>1</td>
      <td>redbone</td>
      <td>0.506826</td>
      <td>True</td>
      <td>miniature_pinscher</td>
      <td>0.074192</td>
      <td>True</td>
      <td>rhodesian_ridgeback</td>
      <td>0.072010</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>891815181378084864</td>
      <td>https://pbs.twimg.com/media/CT4521TWwAEvMyu.jpg</td>
      <td>1</td>
      <td>german_shepherd</td>
      <td>0.596461</td>
      <td>True</td>
      <td>malinois</td>
      <td>0.138584</td>
      <td>True</td>
      <td>bloodhound</td>
      <td>0.116197</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>891689557279858688</td>
      <td>https://pbs.twimg.com/media/CT5Dr8HUEAA-lEu.jpg</td>
      <td>1</td>
      <td>rhodesian_ridgeback</td>
      <td>0.408143</td>
      <td>True</td>
      <td>redbone</td>
      <td>0.360687</td>
      <td>True</td>
      <td>miniature_pinscher</td>
      <td>0.222752</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>891327558926688256</td>
      <td>https://pbs.twimg.com/media/CT5IQmsXIAAKY4A.jpg</td>
      <td>1</td>
      <td>miniature_pinscher</td>
      <td>0.560311</td>
      <td>True</td>
      <td>rottweiler</td>
      <td>0.243682</td>
      <td>True</td>
      <td>doberman</td>
      <td>0.154629</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



### 4 Issue :

Non-descriptive names of columns.



## code


```python
image_clean =image_clean.rename(columns={'jpg_url': 'image_url',
                                                                  'img_num': 'image_number' })
```

## Test


```python
image_clean.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>image_url</th>
      <th>image_number</th>
      <th>p1</th>
      <th>p1_conf</th>
      <th>p1_dog</th>
      <th>p2</th>
      <th>p2_conf</th>
      <th>p2_dog</th>
      <th>p3</th>
      <th>p3_conf</th>
      <th>p3_dog</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>892420643555336193</td>
      <td>https://pbs.twimg.com/media/CT4udn0WwAA0aMy.jpg</td>
      <td>1</td>
      <td>welsh_springer_spaniel</td>
      <td>0.465074</td>
      <td>True</td>
      <td>collie</td>
      <td>0.156665</td>
      <td>True</td>
      <td>shetland_sheepdog</td>
      <td>0.061428</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>892177421306343426</td>
      <td>https://pbs.twimg.com/media/CT42GRgUYAA5iDo.jpg</td>
      <td>1</td>
      <td>redbone</td>
      <td>0.506826</td>
      <td>True</td>
      <td>miniature_pinscher</td>
      <td>0.074192</td>
      <td>True</td>
      <td>rhodesian_ridgeback</td>
      <td>0.072010</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>891815181378084864</td>
      <td>https://pbs.twimg.com/media/CT4521TWwAEvMyu.jpg</td>
      <td>1</td>
      <td>german_shepherd</td>
      <td>0.596461</td>
      <td>True</td>
      <td>malinois</td>
      <td>0.138584</td>
      <td>True</td>
      <td>bloodhound</td>
      <td>0.116197</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>891689557279858688</td>
      <td>https://pbs.twimg.com/media/CT5Dr8HUEAA-lEu.jpg</td>
      <td>1</td>
      <td>rhodesian_ridgeback</td>
      <td>0.408143</td>
      <td>True</td>
      <td>redbone</td>
      <td>0.360687</td>
      <td>True</td>
      <td>miniature_pinscher</td>
      <td>0.222752</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>891327558926688256</td>
      <td>https://pbs.twimg.com/media/CT5IQmsXIAAKY4A.jpg</td>
      <td>1</td>
      <td>miniature_pinscher</td>
      <td>0.560311</td>
      <td>True</td>
      <td>rottweiler</td>
      <td>0.243682</td>
      <td>True</td>
      <td>doberman</td>
      <td>0.154629</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



### 5 Issue :

incorrect some of dogs name like (''one'', "a", "an", "by","very") ,replaced with no name



## code


```python
n_list=['a','an','such','one','quite','very']
for word in n_list:
    tweet_clean.replace(word,'no name',inplace=True)
```

### Test


```python
tweet_clean.name.value_counts()

```




    None        680
    no name      73
    Charlie      11
    Lucy         11
    Oliver       10
               ... 
    Frönq         1
    Simba         1
    Chef          1
    Bilbo         1
    Heinrich      1
    Name: name, Length: 951, dtype: int64



### 6 Issue 

Change Timestamp datatype from Object/String to Datetime

## Code


```python
tweet_clean['timestamp'] = pd.to_datetime(tweet_df['timestamp'])

```

## Test


```python
tweet_clean.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 2175 entries, 0 to 2355
    Data columns (total 12 columns):
     #   Column              Non-Null Count  Dtype              
    ---  ------              --------------  -----              
     0   tweet_id            2175 non-null   object             
     1   timestamp           2175 non-null   datetime64[ns, UTC]
     2   source              2175 non-null   object             
     3   text                2175 non-null   object             
     4   expanded_urls       2117 non-null   object             
     5   rating_numerator    2175 non-null   int64              
     6   rating_denominator  2175 non-null   int64              
     7   name                2175 non-null   object             
     8   doggo               2175 non-null   object             
     9   floofer             2175 non-null   object             
     10  pupper              2175 non-null   object             
     11  puppo               2175 non-null   object             
    dtypes: datetime64[ns, UTC](1), int64(2), object(9)
    memory usage: 285.4+ KB
    

### 7 Issue 


Change Text range to be integer

### Code


```python
json_clean.display_text_range = json_clean.display_text_range.apply(lambda x : x[-1])
```

### Test


```python
json_clean.info()

```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2354 entries, 0 to 2353
    Data columns (total 31 columns):
     #   Column                         Non-Null Count  Dtype              
    ---  ------                         --------------  -----              
     0   created_at                     2354 non-null   datetime64[ns, UTC]
     1   tweet_id                       2354 non-null   int64              
     2   id_str                         2354 non-null   int64              
     3   full_text                      2354 non-null   object             
     4   truncated                      2354 non-null   bool               
     5   display_text_range             2354 non-null   int64              
     6   entities                       2354 non-null   object             
     7   extended_entities              2073 non-null   object             
     8   source                         2354 non-null   object             
     9   in_reply_to_status_id          78 non-null     float64            
     10  in_reply_to_status_id_str      78 non-null     float64            
     11  in_reply_to_user_id            78 non-null     float64            
     12  in_reply_to_user_id_str        78 non-null     float64            
     13  in_reply_to_screen_name        78 non-null     object             
     14  user                           2354 non-null   object             
     15  geo                            0 non-null      float64            
     16  coordinates                    0 non-null      float64            
     17  place                          1 non-null      object             
     18  contributors                   0 non-null      float64            
     19  is_quote_status                2354 non-null   bool               
     20  retweet_count                  2354 non-null   int64              
     21  favorite_count                 2354 non-null   int64              
     22  favorited                      2354 non-null   bool               
     23  retweeted                      2354 non-null   bool               
     24  possibly_sensitive             2211 non-null   float64            
     25  possibly_sensitive_appealable  2211 non-null   float64            
     26  lang                           2354 non-null   object             
     27  retweeted_status               179 non-null    object             
     28  quoted_status_id               29 non-null     float64            
     29  quoted_status_id_str           29 non-null     float64            
     30  quoted_status                  28 non-null     object             
    dtypes: bool(4), datetime64[ns, UTC](1), float64(11), int64(5), object(10)
    memory usage: 505.9+ KB
    

### 8 Issue 

8.rating's numerator and denominator should be calculated in one column then change the type to be float.

## code


```python
tweet_clean['rating_numerator']= tweet_clean['rating_numerator'].astype(float)
tweet_clean['rating_denominator']= tweet_clean['rating_denominator'].astype(float)
tweet_clean['rating'] = tweet_clean['rating_numerator']/tweet_clean['rating_denominator']
```


```python
tweet_clean.drop(['rating_numerator' , 'rating_denominator'], axis=1 , inplace=True)
```


```python
tweet_clean['tweet_id'] = tweet_clean['tweet_id'].astype(str)
```

## Test


```python

tweet_clean.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>timestamp</th>
      <th>source</th>
      <th>text</th>
      <th>expanded_urls</th>
      <th>name</th>
      <th>doggo</th>
      <th>floofer</th>
      <th>pupper</th>
      <th>puppo</th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>892420643555336193</td>
      <td>2017-08-01 16:23:56+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Phineas. He's a mystical boy. Only eve...</td>
      <td>https://twitter.com/dog_rates/status/892420643...</td>
      <td>Phineas</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>1.3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>892177421306343426</td>
      <td>2017-08-01 00:17:27+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Tilly. She's just checking pup on you....</td>
      <td>https://twitter.com/dog_rates/status/892177421...</td>
      <td>Tilly</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>1.3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>891815181378084864</td>
      <td>2017-07-31 00:18:03+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Archie. He is a rare Norwegian Pouncin...</td>
      <td>https://twitter.com/dog_rates/status/891815181...</td>
      <td>Archie</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>891689557279858688</td>
      <td>2017-07-30 15:58:51+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Darla. She commenced a snooze mid meal...</td>
      <td>https://twitter.com/dog_rates/status/891689557...</td>
      <td>Darla</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>1.3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>891327558926688256</td>
      <td>2017-07-29 16:00:24+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Franklin. He would like you to stop ca...</td>
      <td>https://twitter.com/dog_rates/status/891327558...</td>
      <td>Franklin</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>1.2</td>
    </tr>
  </tbody>
</table>
</div>



## Tidiness


### 1 Issue 


Create one column for dog stags(doggo, floofer, pupper, puppo)


```python
tweet_clean.doggo.replace('None', '', inplace=True)
tweet_clean.floofer.replace('None', '', inplace=True)
tweet_clean.pupper.replace('None', '', inplace=True)
tweet_clean.puppo.replace('None', '', inplace=True)

tweet_clean.doggo.replace(np.NaN, '', inplace=True)
tweet_clean.floofer.replace(np.NaN, '', inplace=True)
tweet_clean.pupper.replace(np.NaN, '', inplace=True)
tweet_clean.puppo.replace(np.NaN, '', inplace=True)
```


```python
tweet_clean['stage'] = tweet_clean.doggo + tweet_clean.floofer + tweet_clean.pupper + tweet_clean.puppo
tweet_clean.loc[tweet_clean.stage == 'doggopupper', 'stage'] = 'doggo, pupper'
tweet_clean.loc[tweet_clean.stage == 'doggopuppo', 'stage'] = 'doggo, puppo'
tweet_clean.loc[tweet_clean.stage == 'doggofloofer', 'stage'] = 'doggo, floofer'
```


```python

```

### Test


```python
tweet_clean

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweet_id</th>
      <th>timestamp</th>
      <th>source</th>
      <th>text</th>
      <th>expanded_urls</th>
      <th>name</th>
      <th>doggo</th>
      <th>floofer</th>
      <th>pupper</th>
      <th>puppo</th>
      <th>rating</th>
      <th>stage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>892420643555336193</td>
      <td>2017-08-01 16:23:56+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Phineas. He's a mystical boy. Only eve...</td>
      <td>https://twitter.com/dog_rates/status/892420643...</td>
      <td>Phineas</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>1.3</td>
      <td></td>
    </tr>
    <tr>
      <th>1</th>
      <td>892177421306343426</td>
      <td>2017-08-01 00:17:27+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Tilly. She's just checking pup on you....</td>
      <td>https://twitter.com/dog_rates/status/892177421...</td>
      <td>Tilly</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>1.3</td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>891815181378084864</td>
      <td>2017-07-31 00:18:03+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Archie. He is a rare Norwegian Pouncin...</td>
      <td>https://twitter.com/dog_rates/status/891815181...</td>
      <td>Archie</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>1.2</td>
      <td></td>
    </tr>
    <tr>
      <th>3</th>
      <td>891689557279858688</td>
      <td>2017-07-30 15:58:51+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Darla. She commenced a snooze mid meal...</td>
      <td>https://twitter.com/dog_rates/status/891689557...</td>
      <td>Darla</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>1.3</td>
      <td></td>
    </tr>
    <tr>
      <th>4</th>
      <td>891327558926688256</td>
      <td>2017-07-29 16:00:24+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is Franklin. He would like you to stop ca...</td>
      <td>https://twitter.com/dog_rates/status/891327558...</td>
      <td>Franklin</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>1.2</td>
      <td></td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2351</th>
      <td>666049248165822465</td>
      <td>2015-11-16 00:24:50+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here we have a 1949 1st generation vulpix. Enj...</td>
      <td>https://twitter.com/dog_rates/status/666049248...</td>
      <td>None</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>0.5</td>
      <td></td>
    </tr>
    <tr>
      <th>2352</th>
      <td>666044226329800704</td>
      <td>2015-11-16 00:04:52+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is a purebred Piers Morgan. Loves to Netf...</td>
      <td>https://twitter.com/dog_rates/status/666044226...</td>
      <td>no name</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>0.6</td>
      <td></td>
    </tr>
    <tr>
      <th>2353</th>
      <td>666033412701032449</td>
      <td>2015-11-15 23:21:54+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here is a very happy pup. Big fan of well-main...</td>
      <td>https://twitter.com/dog_rates/status/666033412...</td>
      <td>no name</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>0.9</td>
      <td></td>
    </tr>
    <tr>
      <th>2354</th>
      <td>666029285002620928</td>
      <td>2015-11-15 23:05:30+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>This is a western brown Mitsubishi terrier. Up...</td>
      <td>https://twitter.com/dog_rates/status/666029285...</td>
      <td>no name</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>0.7</td>
      <td></td>
    </tr>
    <tr>
      <th>2355</th>
      <td>666020888022790149</td>
      <td>2015-11-15 22:32:08+00:00</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>Here we have a Japanese Irish Setter. Lost eye...</td>
      <td>https://twitter.com/dog_rates/status/666020888...</td>
      <td>None</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>0.8</td>
      <td></td>
    </tr>
  </tbody>
</table>
<p>2175 rows × 12 columns</p>
</div>



### 2 Issue 


Merging all dataframes into one data frame



### code


```python
mdf = pd.merge(df_json, tweet_df, on='tweet_id', how='left')
mdf = pd.merge(mdf, image_df, on='tweet_id', how='left')

```

### Test mdf


```python
mdf
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>created_at</th>
      <th>tweet_id</th>
      <th>id_str</th>
      <th>full_text</th>
      <th>truncated</th>
      <th>display_text_range</th>
      <th>entities</th>
      <th>extended_entities</th>
      <th>source_x</th>
      <th>in_reply_to_status_id_x</th>
      <th>...</th>
      <th>img_num</th>
      <th>p1</th>
      <th>p1_conf</th>
      <th>p1_dog</th>
      <th>p2</th>
      <th>p2_conf</th>
      <th>p2_dog</th>
      <th>p3</th>
      <th>p3_conf</th>
      <th>p3_dog</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-08-01 16:23:56+00:00</td>
      <td>892420643555336193</td>
      <td>892420643555336192</td>
      <td>This is Phineas. He's a mystical boy. Only eve...</td>
      <td>False</td>
      <td>[0, 85]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 892420639486877696, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>1.0</td>
      <td>orange</td>
      <td>0.097049</td>
      <td>False</td>
      <td>bagel</td>
      <td>0.085851</td>
      <td>False</td>
      <td>banana</td>
      <td>0.076110</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-08-01 00:17:27+00:00</td>
      <td>892177421306343426</td>
      <td>892177421306343424</td>
      <td>This is Tilly. She's just checking pup on you....</td>
      <td>False</td>
      <td>[0, 138]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 892177413194625024, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>1.0</td>
      <td>Chihuahua</td>
      <td>0.323581</td>
      <td>True</td>
      <td>Pekinese</td>
      <td>0.090647</td>
      <td>True</td>
      <td>papillon</td>
      <td>0.068957</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-07-31 00:18:03+00:00</td>
      <td>891815181378084864</td>
      <td>891815181378084864</td>
      <td>This is Archie. He is a rare Norwegian Pouncin...</td>
      <td>False</td>
      <td>[0, 121]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 891815175371796480, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>1.0</td>
      <td>Chihuahua</td>
      <td>0.716012</td>
      <td>True</td>
      <td>malamute</td>
      <td>0.078253</td>
      <td>True</td>
      <td>kelpie</td>
      <td>0.031379</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017-07-30 15:58:51+00:00</td>
      <td>891689557279858688</td>
      <td>891689557279858688</td>
      <td>This is Darla. She commenced a snooze mid meal...</td>
      <td>False</td>
      <td>[0, 79]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 891689552724799489, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>1.0</td>
      <td>paper_towel</td>
      <td>0.170278</td>
      <td>False</td>
      <td>Labrador_retriever</td>
      <td>0.168086</td>
      <td>True</td>
      <td>spatula</td>
      <td>0.040836</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-07-29 16:00:24+00:00</td>
      <td>891327558926688256</td>
      <td>891327558926688256</td>
      <td>This is Franklin. He would like you to stop ca...</td>
      <td>False</td>
      <td>[0, 138]</td>
      <td>{'hashtags': [{'text': 'BarkWeek', 'indices': ...</td>
      <td>{'media': [{'id': 891327551943041024, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>2.0</td>
      <td>basset</td>
      <td>0.555712</td>
      <td>True</td>
      <td>English_springer</td>
      <td>0.225770</td>
      <td>True</td>
      <td>German_short-haired_pointer</td>
      <td>0.175219</td>
      <td>True</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2349</th>
      <td>2015-11-16 00:24:50+00:00</td>
      <td>666049248165822465</td>
      <td>666049248165822464</td>
      <td>Here we have a 1949 1st generation vulpix. Enj...</td>
      <td>False</td>
      <td>[0, 120]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 666049244999131136, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>1.0</td>
      <td>miniature_pinscher</td>
      <td>0.560311</td>
      <td>True</td>
      <td>Rottweiler</td>
      <td>0.243682</td>
      <td>True</td>
      <td>Doberman</td>
      <td>0.154629</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2350</th>
      <td>2015-11-16 00:04:52+00:00</td>
      <td>666044226329800704</td>
      <td>666044226329800704</td>
      <td>This is a purebred Piers Morgan. Loves to Netf...</td>
      <td>False</td>
      <td>[0, 137]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 666044217047650304, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>1.0</td>
      <td>Rhodesian_ridgeback</td>
      <td>0.408143</td>
      <td>True</td>
      <td>redbone</td>
      <td>0.360687</td>
      <td>True</td>
      <td>miniature_pinscher</td>
      <td>0.222752</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2351</th>
      <td>2015-11-15 23:21:54+00:00</td>
      <td>666033412701032449</td>
      <td>666033412701032448</td>
      <td>Here is a very happy pup. Big fan of well-main...</td>
      <td>False</td>
      <td>[0, 130]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 666033409081393153, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>1.0</td>
      <td>German_shepherd</td>
      <td>0.596461</td>
      <td>True</td>
      <td>malinois</td>
      <td>0.138584</td>
      <td>True</td>
      <td>bloodhound</td>
      <td>0.116197</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2352</th>
      <td>2015-11-15 23:05:30+00:00</td>
      <td>666029285002620928</td>
      <td>666029285002620928</td>
      <td>This is a western brown Mitsubishi terrier. Up...</td>
      <td>False</td>
      <td>[0, 139]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 666029276303482880, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>1.0</td>
      <td>redbone</td>
      <td>0.506826</td>
      <td>True</td>
      <td>miniature_pinscher</td>
      <td>0.074192</td>
      <td>True</td>
      <td>Rhodesian_ridgeback</td>
      <td>0.072010</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2353</th>
      <td>2015-11-15 22:32:08+00:00</td>
      <td>666020888022790149</td>
      <td>666020888022790144</td>
      <td>Here we have a Japanese Irish Setter. Lost eye...</td>
      <td>False</td>
      <td>[0, 131]</td>
      <td>{'hashtags': [], 'symbols': [], 'user_mentions...</td>
      <td>{'media': [{'id': 666020881337073664, 'id_str'...</td>
      <td>&lt;a href="http://twitter.com/download/iphone" r...</td>
      <td>NaN</td>
      <td>...</td>
      <td>1.0</td>
      <td>Welsh_springer_spaniel</td>
      <td>0.465074</td>
      <td>True</td>
      <td>collie</td>
      <td>0.156665</td>
      <td>True</td>
      <td>Shetland_sheepdog</td>
      <td>0.061428</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
<p>2354 rows × 58 columns</p>
</div>



# Storing Data


Save gathered, assessed, and cleaned master dataset to a CSV file named "twitter_archive_master.csv".



## Name It : mdf



```python
mdf.to_csv('twitter_archive_master.csv', index=False, encoding = 'utf-8')
```

# Analyzing and Visualizing Data

In this section, analyze and visualize your wrangled data. You must produce at least three (3) insights and one (1) visualization.



## Insights:


 1.P1 algorithm has the highest confidence rate than other algorithms.

2. charlieie  is the most popular dog name

3 .Puppy has the average highest rating, retweet and favorite.




## Visualization

1.P1 algorithm has the highest confidence rate than other algorithms


```python
plt.figure(figsize=(15,10))
mdf.p1_conf.hist(alpha=0.5, bins=100, label = 'p1', color='yellow')
mdf.p2_conf.hist(alpha=0.5, bins=100, label = 'p2', color='black')
mdf.p3_conf.hist(alpha=0.5, bins=100, label = 'p3', color='blue')
plt.title('The highest confident algorithm')
plt.legend(loc = 'upper right', fontsize=13)
plt.show()
```


    
![png](output_144_0.png)
    


Looking at the figure above we see, that p1 algorithm has the highest confident and p3 algorithm has the lowest.



2.charlieie is the most popular dog name


```python
# charlie is the most popular dog name
mdf.name.value_counts()[2:8].plot(kind='barh', figsize=(15,8), 
                                 title='common dog names');
```


    
![png](output_147_0.png)
    


Looking at the figure above we see, charlieie is the most popular dog name

# Conclusions :


The dataset that I was wrangling (and analyzing and visualizing) is the tweet archive of Twitter user @dog_rates, also known as WeRateDogs.

WeRateDogs is a Twitter account that rates people's dogs with a humorous comment about the dog

If you are looking to adopt a dog , Most popular type is pupper.



```python

```
