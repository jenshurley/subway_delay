

```python
import tweepy
import pandas as pd

# Get frequency for each train being late
# https://twitter.com/subwaystats
#get last 1000, ant if you see "delay" in text, 
# value counts on a series
```


```python
consumer_key = 
consumer_secret = 
app_key = 
app_secret = 

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(app_key, app_secret)
api = tweepy.API(auth)
```


```python
subway_stats = []

for status in tweepy.Cursor(api.user_timeline, id='subwaystats').items(1000):
    subway_stats.append(status)
```


```python
len(subway_stats)
```




    1000




```python
subway_stats[0]._json
```




    {'contributors': None,
     'coordinates': None,
     'created_at': 'Fri Jun 22 01:10:04 +0000 2018',
     'entities': {'hashtags': [{'indices': [0, 7], 'text': 'Ntrain'},
       {'indices': [8, 15], 'text': 'Qtrain'},
       {'indices': [16, 23], 'text': 'Rtrain'},
       {'indices': [24, 31], 'text': 'Wtrain'}],
      'symbols': [],
      'urls': [{'display_url': 'twitter.com/i/web/status/1…',
        'expanded_url': 'https://twitter.com/i/web/status/1009966719337750528',
        'indices': [117, 140],
        'url': 'https://t.co/F0agVK05jd'}],
      'user_mentions': []},
     'favorite_count': 0,
     'favorited': False,
     'geo': None,
     'id': 1009966719337750528,
     'id_str': '1009966719337750528',
     'in_reply_to_screen_name': None,
     'in_reply_to_status_id': None,
     'in_reply_to_status_id_str': None,
     'in_reply_to_user_id': None,
     'in_reply_to_user_id_str': None,
     'is_quote_status': False,
     'lang': 'en',
     'place': None,
     'possibly_sensitive': False,
     'retweet_count': 0,
     'retweeted': False,
     'source': '<a href="http://www.subwaystats.com" rel="nofollow">SubwayStats</a>',
     'text': '#Ntrain #Qtrain #Rtrain #Wtrain have service change Bay Ridge-bound [R] trains run via the [Q] from Canal St, Manha… https://t.co/F0agVK05jd',
     'truncated': True,
     'user': {'contributors_enabled': False,
      'created_at': 'Mon May 28 22:39:13 +0000 2012',
      'default_profile': False,
      'default_profile_image': False,
      'description': 'Current #NYC #MTA #subway status, delays and closures. Visit https://t.co/EKcEGv271h for detailed statistics by line.',
      'entities': {'description': {'urls': [{'display_url': 'subwaystats.com',
          'expanded_url': 'https://subwaystats.com',
          'indices': [61, 84],
          'url': 'https://t.co/EKcEGv271h'}]},
       'url': {'urls': [{'display_url': 'subwaystats.com',
          'expanded_url': 'https://subwaystats.com',
          'indices': [0, 23],
          'url': 'https://t.co/EKcEGv271h'}]}},
      'favourites_count': 30,
      'follow_request_sent': False,
      'followers_count': 4652,
      'following': False,
      'friends_count': 134,
      'geo_enabled': False,
      'has_extended_profile': False,
      'id': 593125784,
      'id_str': '593125784',
      'is_translation_enabled': False,
      'is_translator': False,
      'lang': 'en',
      'listed_count': 44,
      'location': 'New York, NY, USA',
      'name': 'Subway Status Delays',
      'notifications': False,
      'profile_background_color': '000000',
      'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png',
      'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png',
      'profile_background_tile': False,
      'profile_banner_url': 'https://pbs.twimg.com/profile_banners/593125784/1474882712',
      'profile_image_url': 'http://pbs.twimg.com/profile_images/995383229237542912/EqxE9E2C_normal.jpg',
      'profile_image_url_https': 'https://pbs.twimg.com/profile_images/995383229237542912/EqxE9E2C_normal.jpg',
      'profile_link_color': 'ABB8C2',
      'profile_sidebar_border_color': '000000',
      'profile_sidebar_fill_color': '000000',
      'profile_text_color': '000000',
      'profile_use_background_image': False,
      'protected': False,
      'screen_name': 'SubwayStats',
      'statuses_count': 63527,
      'time_zone': None,
      'translator_type': 'none',
      'url': 'https://t.co/EKcEGv271h',
      'utc_offset': None,
      'verified': True}}




```python
df = pd.DataFrame([x._json for x in subway_stats])[['text', 'created_at', 'entities']]
```


```python
df.head()
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
      <th>text</th>
      <th>created_at</th>
      <th>entities</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>#Ntrain #Qtrain #Rtrain #Wtrain have service c...</td>
      <td>Fri Jun 22 01:10:04 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Ntrain', 'indices': [0...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>#Btrain #Dtrain #Ftrain #Mtrain have service c...</td>
      <td>Fri Jun 22 01:10:03 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Btrain', 'indices': [0...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>#Ntrain #Qtrain #Rtrain #Wtrain have delays Ba...</td>
      <td>Fri Jun 22 00:55:05 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Ntrain', 'indices': [0...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>#Btrain #Dtrain #Ftrain #Mtrain have delays [B...</td>
      <td>Fri Jun 22 00:55:04 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Btrain', 'indices': [0...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>#Atrain #Ctrain and #Etrain have planned work ...</td>
      <td>Fri Jun 22 00:55:03 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Atrain', 'indices': [0...</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['train_type'] = df['entities'].map(lambda x: x.get('hashtags')[0].get('text'))
```


```python
df.head()
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
      <th>text</th>
      <th>created_at</th>
      <th>entities</th>
      <th>train_type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>#Ntrain #Qtrain #Rtrain #Wtrain have service c...</td>
      <td>Fri Jun 22 01:10:04 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Ntrain', 'indices': [0...</td>
      <td>Ntrain</td>
    </tr>
    <tr>
      <th>1</th>
      <td>#Btrain #Dtrain #Ftrain #Mtrain have service c...</td>
      <td>Fri Jun 22 01:10:03 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Btrain', 'indices': [0...</td>
      <td>Btrain</td>
    </tr>
    <tr>
      <th>2</th>
      <td>#Ntrain #Qtrain #Rtrain #Wtrain have delays Ba...</td>
      <td>Fri Jun 22 00:55:05 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Ntrain', 'indices': [0...</td>
      <td>Ntrain</td>
    </tr>
    <tr>
      <th>3</th>
      <td>#Btrain #Dtrain #Ftrain #Mtrain have delays [B...</td>
      <td>Fri Jun 22 00:55:04 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Btrain', 'indices': [0...</td>
      <td>Btrain</td>
    </tr>
    <tr>
      <th>4</th>
      <td>#Atrain #Ctrain and #Etrain have planned work ...</td>
      <td>Fri Jun 22 00:55:03 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Atrain', 'indices': [0...</td>
      <td>Atrain</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.train_type.value_counts()
```




    Btrain      211
    4train      197
    Ntrain      153
    Atrain      141
    1train      118
    7train       50
    Ltrain       34
    Jtrain       31
    SIRtrain     26
    Gtrain       22
    Strain       15
    ltrain        1
    Ltrains       1
    Name: train_type, dtype: int64




```python
#if text 'delay' not in text, drop row
#mask
mask = df.text.map(lambda x: True if 'delays' in x else False)
```


```python
mask.value_counts()
```




    False    725
    True     275
    Name: text, dtype: int64




```python
type(mask)
```




    pandas.core.series.Series




```python
mask[:10]
```




    0    False
    1    False
    2     True
    3     True
    4    False
    5    False
    6    False
    7    False
    8    False
    9     True
    Name: text, dtype: bool




```python
df_delay = df[mask]
```


```python
df_delay.head()
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
      <th>text</th>
      <th>created_at</th>
      <th>entities</th>
      <th>train_type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>#Ntrain #Qtrain #Rtrain #Wtrain have delays Ba...</td>
      <td>Fri Jun 22 00:55:05 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Ntrain', 'indices': [0...</td>
      <td>Ntrain</td>
    </tr>
    <tr>
      <th>3</th>
      <td>#Btrain #Dtrain #Ftrain #Mtrain have delays [B...</td>
      <td>Fri Jun 22 00:55:04 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Btrain', 'indices': [0...</td>
      <td>Btrain</td>
    </tr>
    <tr>
      <th>9</th>
      <td>#Btrain #Dtrain #Ftrain #Mtrain have delays [B...</td>
      <td>Fri Jun 22 00:15:03 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Btrain', 'indices': [0...</td>
      <td>Btrain</td>
    </tr>
    <tr>
      <th>12</th>
      <td>#Jtrain and #Ztrain have delays  #NYCsubway ht...</td>
      <td>Fri Jun 22 00:05:06 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Jtrain', 'indices': [0...</td>
      <td>Jtrain</td>
    </tr>
    <tr>
      <th>13</th>
      <td>#Btrain #Dtrain #Ftrain #Mtrain have delays [B...</td>
      <td>Fri Jun 22 00:05:02 +0000 2018</td>
      <td>{'hashtags': [{'text': 'Btrain', 'indices': [0...</td>
      <td>Btrain</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_delay.train_type.value_counts()
```




    Btrain      59
    4train      50
    Ntrain      43
    Atrain      37
    1train      32
    7train      17
    Jtrain      13
    Ltrain       9
    Gtrain       6
    Strain       5
    SIRtrain     4
    Name: train_type, dtype: int64


