# Twitter sentiment analysis: LIVE

The challenge is about to create amazing stream tweets sentiment analysis dashboards from Portuguese language. This repository is based on [Sentdex-socialsentiment](https://github.com/Sentdex/socialsentiment)

<p align="center">
<img src="https://github.com/Alro10/twitter-sentiment-live/blob/master/live.png" alt="alt text" width="100%" height="100%">
</p>

## Description

- Streaming tweets writing in Portuguese, [tweepy](https://github.com/tweepy/tweepy).
- Translate to English using [py-googletrans](https://github.com/ssut/py-googletrans).
- Sentiment analysis with [VADER approach](https://www.aaai.org/ocs/index.php/ICWSM/ICWSM14/paper/download/8109/8122) [[Python implementation](https://github.com/cjhutto/vaderSentiment)]. All tweets being classified in just two classes: Positive and Negative.
- Make dashboards using dash an plotly.

## Contents

- `dash_mess.py` - This is currently the main front-end application code. Contains the dash application layouts, logic for graphs, interfaces with the database...etc. This code is setup to run on a flask instance. If you want to clone this and run it locally, you will be using the `dev_server.py`

- `dev_server.py` - If you wish to run this application locally, on the dev server, run via this instead.

- `twitter_stream.py` - This should run in the background of your application. This is what streams tweets from Twitter, storing them into the sqlite3 database. If you want to classify tweets in other language just change `languages=["pt"]` and `track=["a","e","i","o","u"]` in `twitterStream.filter()`

- `config.py` - Meant for many configurations, but right now it just contains stop words. Words we don't intend to ever count in the "trending"

- `cache.py` -  For caching purposes in effort to get things to run faster.

- `db-truncate.py` - A script to truncate the infinitely-growing sqlite3 database. You will get about 3.5 millions tweets per day, depending on how fast you can process. You can keep these, but, as the database grows, search times will dramatically suffer.

## Quick compilation

- Clone repository: `git clone https://github.com/Alro10/twitter-sentiment-live.git`
- Install requirements using `pip3 install -r requirements.txt` or

  - Install in virtual environment:
    ```
    sudo apt install python3-venv

    python3 -m venv env

    source env/bin/activate

    pip install -r requirements.txt    

    ```

- Fill in your Twitter App credentials to `twitter_stream.py`. Go to [**apps.twitter.com**](https://apps.twitter.com/) to set that up if you need to.
- Run `twitter_stream.py` to build database and after running `dev_server.py`, since you need the database. If you're using this locally.
- If you want to deploy this to a webserver, see [**deploying Dash application tutorial**](https://pythonprogramming.net/deploy-vps-dash-data-visualization/)
- You might need the latest version of sqlite3. Install as follows to avoid some issues.

```
sudo add-apt-repository ppa:jonathonf/backports
sudo apt-get update && sudo apt-get install sqlite3
```
- Consider running the `db-truncate.py` from time to time (or via a cronjob), to keep the database reasonably sized. In its current state, the database really doesn't need to store more than 2-3 days of data most likely.

## TODO

- This app uses googletrans API, see requirements, and an issue sometimes occurs when you called the API and apparently the reason may be the proxy configuration. Described in [googletrans/issue](https://github.com/ssut/py-googletrans/issues/113) but not solved yet.
```
raise JSONDecodeError("Expecting value", s, err.value) from None
json.decoder.JSONDecodeError: Expecting value: line 1 column 1 (char 0)
```
- Deploy on webserver.
- Run inside docker containers.
- Add neutral sentiment, that is possible since VADER is able to do.
- Use other approaches for sentiment analysis, such as ConvNets, LSTM, etc. But we will need a database in Portuguese for training the algorithm, I didn't find a good database.

*Send a pull request or open an issue are very welcome!* :+1:
