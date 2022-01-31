<p align="center"><a href="https://github.com/fabston/TradingView-Webhook-Bot" target="_blank"><img src="https://raw.githubusercontent.com/fabston/TradingView-Webhook-Bot/master/assets/logo.png"></a></p>

<p align="center">
    <a href="https://www.python.org/downloads/release/python-380/"><img src="https://img.shields.io/badge/python-3.8-blue.svg?style=plastic" alt="Python version"></a>
    <a href="https://github.com/fabston/TradingView-Webhook-Bot/blob/master/LICENSE"><img src="https://img.shields.io/github/license/fabston/TradingView-Webhook-Bot?style=plastic" alt="GitHub license"></a>
    <a href="https://github.com/fabston/TradingView-Webhook-Bot/issues"><img src="https://img.shields.io/github/issues/fabston/TradingView-Webhook-Bot?style=plastic" alt="GitHub issues"></a>
    <a href="https://github.com/fabston/TradingView-Webhook-Bot/pulls"><img src="https://img.shields.io/github/issues-pr/fabston/TradingView-Webhook-Bot?style=plastic" alt="GitHub pull requests"></a>
    <br /><a href="https://github.com/fabston/TradingView-Webhook-Bot/stargazers"><img src="https://img.shields.io/github/stars/fabston/TradingView-Webhook-Bot?style=social" alt="GitHub stars"></a>
    <a href="https://github.com/fabston/TradingView-Webhook-Bot/network/members"><img src="https://img.shields.io/github/forks/fabston/TradingView-Webhook-Bot?style=social" alt="GitHub forks"></a>
    <a href="https://github.com/fabston/TradingView-Webhook-Bot/watchers"><img src="https://img.shields.io/github/watchers/fabston/TradingView-Webhook-Bot?style=social" alt="GitHub watchers"></a>
</p>

<p align="center">
  <a href="#about">About</a>
  •
  <a href="#features">Features</a>
  •
  <a href="#installation">Installation</a>
  •
  <a href="#images">Images</a>
  •
  <a href="#how-can-i-help">Help</a>
</p>

## About
The **TradingView Webhook Bot** ⚙️ listens to [TradingView](https://tradingview.com) alerts via [webhooks](https://www.tradingview.com/support/solutions/43000529348-i-want-to-know-more-about-webhooks/) using [flask](https://flask.palletsprojects.com/en/1.1.x/).
All alerts can be instantly sent to Telegram, Discord, Twitter and/or Email.

## Features
- Telegram Support using the [Python Telegram](https://github.com/python-telegram-bot/python-telegram-bot) libary
- Discord Support using [webhooks](https://support.discord.com/hc/de/articles/228383668-Webhooks-verwenden)
- Slack Support using [webhooks](https://api.slack.com/messaging/webhooks)
- Twitter Support using the [tweepy](https://github.com/tweepy/tweepy) libary
- Email Support using [smtplib](https://docs.python.org/3/library/smtplib.html)
- Alert channels can be enabled or disabled in [`config.py`](https://github.com/fabston/TradingView-Webhook-Bot/blob/master/config.py)
- Dynamically send alerts to different Telegram and/or Discord channels
- TradingView `{{close}}`, `{{exchange}}` etc. variables support. Read more [here](https://www.tradingview.com/blog/en/introducing-variables-in-alerts-14880/)

> 💡 Got a feature idea? Open an [issue](https://github.com/fabston/TradingView-Webhook-Bot/issues/new?assignees=&labels=enhancement&template=feature-request---.md) and I might implement it.

## Installation
>On any VPS
1. Clone this repository `git clone https://github.com/fabston/TradingView-Webhook-Bot.git`
1. Create your virtual environment `python3 -m venv TradingView-Webhook-Bot`
1. Activate it `source TradingView-Webhook-Bot/bin/activate && cd TradingView-Webhook-Bot`
1. Install all requirements `pip install -r requirements.txt`
1. Edit and update [`config.py`](https://github.com/fabston/TradingView-Webhook-Bot/blob/master/config.py)
1. The Telegram ID should be set as an integer, but in some cases it is needed to define it as a sting, and to set the Channel name (@MyChannel) insteed of the Channel ID (-1001277977502).
1. Setup TradingView alerts. An example alert message would be:
    ```json
    {
     "key": "9T2q394M92",
     "telegram": "-1001277977502",
     "discord": "789842341870960670/BFeBBrCt-w2Z9RJ2wlH6TWUjM5bJuC29aJaJ5OQv9sE6zCKY_AlOxxFwRURkgEl852s3",
     "slack": "T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX",
     "msg": "Long *#{{ticker}}* at `{{close}}`"
    }
    ```
    - `key` is mandatory! It has to match with `sec_key` in [`config.py`](https://github.com/fabston/TradingView-Webhook-Bot/blob/master/config.py). It's an extra security measurement to ensure nobody else is executing your alerts
    - `telegram`, `discord`, `slack` is optional. If it is not set it will fall back to the config.py settings
    - `msg` can be anything. Markdown for [Telegram](https://core.telegram.org/api/entities) and [Discord](https://support.discord.com/hc/en-us/articles/210298617-Markdown-Text-101-Chat-Formatting-Bold-Italic-Underline-) is supported as well
        - TradingViews variables like `{{close}}`, `{{exchange}}` etc. work too. More can be found [here](https://www.tradingview.com/blog/en/introducing-variables-in-alerts-14880/)
    - Your webhook url would be `http://<YOUR-IP>/webhook`
1. If you use a firewall be sure to open the corresponding port
1. TradingView POST Request are made from the bellow IP Source :
1. TradingView Ref : https://www.tradingview.com/?solution=43000529348
1. 52.89.214.238
34.212.75.30
54.218.53.128
52.32.178.7
1. Run the bot with `python main.py`

### Create a service

1. Create a /root/startbot.sh
1. Create a directory for logs : mkdir /root/TradingView-Webhook-Bot/logs
1. Create a service file : /etc/systemd/system/telegrambotservice.service
1. Start the service : systemctl start telegrambotservice.service

1. You can stop or check the status of the service with the command bellow
1. systemctl stop telegrambotservice.service
1. systemctl status telegrambotservice.service



### Docker
1. Clone this repository `git clone https://github.com/fabston/TradingView-Webhook-Bot.git`
1. Edit and update [`config.py`](https://github.com/fabston/TradingView-Webhook-Bot/blob/master/config.py)
1. `docker-compose build`
1. `docker-compose up`

*It is recommended to run flask on a different port like 8080. It is then necessary to forward port 80 to 8080.*

## Images
![Webhook Bot](https://i.imgur.com/vZA42cc.png)

## How can I help?
All kinds of contributions are welcome 🙌! The most basic way to show your support is to `⭐️ star` the project, or raise [`🐞 issues`](https://github.com/fabston/TradingView-Webhook-Bot/issues/new/choose).

***

<p align="center">
    <a href="https://www.buymeacoffee.com/fabston"><img alt="Buy Me A Coffee" title="☕️" src="https://raw.githubusercontent.com/fabston/TradingView-Webhook-Bot/master/assets/bmac.png" width=200px></a>
</p>
