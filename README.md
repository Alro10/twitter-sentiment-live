# IBM data science test

The challenge is about to create amazing tweets sentiment analysis dashboards from Portuguese language, specific Brazil. The app classifies stream tweets writing in Portuguese and show a real-time dashboard.

## Contents

- `dash_mess.py` - This is currently the main front-end application code. Contains the dash application layouts, logic for graphs, interfaces with the database...etc. Name is descriptive of the overall state of code :) ...this code is setup to run on a flask instance. If you want to clone this and run it locally, you will be using the `dev_server.py`

- `dev_server.py` - If you wish to run this application locally, on the dev server, run via this instead.

- `twitter_stream.py` - This should run in the background of your application. This is what streams tweets from Twitter, storing them into the sqlite3 database, which is what the `dash_mess.py` file interfaces with.

- `config.py` - Meant for many configurations, but right now it just contains stop words. Words we don't intend to ever count in the "trending"

- `cache.py` -  For caching purposes in effort to get things to run faster.

- `db-truncate.py` - A script to truncate the infinitely-growing sqlite database. You will get about 3.5 millionish tweets per day, depending on how fast you can process. You can keep these, but, as the database grows, search times will dramatically suffer.

## Quick compilation

- Clone repository: `git clone https://github.com/Alro10/twitter-sentiment-live.git`
- Install `requirements.txt` using `pip3 install -r requirements.txt`
  - It is recommending to install in virtual environment:
    ```
    sudo apt install python3-venv

    python3 -m venv env

    source env/bin/activate    

    ```

- Fill in your Twitter App credentials to `twitter_stream.py`. Go to [**apps.twitter.com**](https://apps.twitter.com/) to set that up if you need to.
- Run `twitter_stream.py` to build database
- If you're using this locally, you can run the application with the `dev_server.py` script. If you want to deploy this to a webserver, see my [**deploying Dash application tutorial**](https://pythonprogramming.net/deploy-vps-dash-data-visualization/)
- You might need the latest version of sqlite3. Install as follows to avoid some issues

```
sudo add-apt-repository ppa:jonathonf/backports
sudo apt-get update && sudo apt-get install sqlite3
```
- Consider running the `db-truncate.py` from time to time (or via a cronjob), to keep the database reasonably sized. In its current state, the database really doesn't need to store more than 2-3 days of data most likely.
