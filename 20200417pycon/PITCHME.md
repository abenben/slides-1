## Automate the Boring Stuff with Slackbot

### Takanori Suzuki

PyCon / 2020 Apr 17

Note:

* Thank you for taking the time to watch my talk.
* I am very happy to be able to talk at PyCon.

---

## Agenda

* @color[SeaGreen](Background) and @color[SeaGreen](Motivation) for Slackbot
* How to create @color[SeaGreen](Simple) bot
* How to create @color[SeaGreen](Interactive) bot
* How to @color[SeaGreen](Extend) bot using libs and APIs

Note:
Today, I will talk about...

---

## Tweets 🐦 👍

`#pycon2020` / `@takanory`

Note:
* I'd be happy to give you feedback on Twitter, etc.
* Before the main topic,...I will introduce mycelf.

---

## Who am I?

* Takanori Suzuki / 鈴木 たかのり
* @fab[twitter] [@takanory](https://twitter.com/takanory)
* [PyCon JP Association](https://www.pycon.jp)
* [BeProud Inc.](https://www.beproud.jp)
* [Python Boot Camp](https://www.pycon.jp/support/bootcamp.html), [Python mini Hack-a-thon](https://pyhack.connpass.com/), [Python Bouldering Club](https://kabepy.connpass.com/)

![takanory](assets/images/sokidan-square.jpg)

Note:
(1m)
* Before the main topic,...I will introduce mycelf.
* I'm Takanori Suzuki. My twitter is "takanory", please follow me.
* I'm Vice-Chairperson of PyCon JP Association.
* Last year,... I was challenged to talk or poster at Python Conference around the world, which I called PyCon tour.

+++?image=20191010pyconsg/images/pycontourmap.jpg&size=auto 90%

@snap[south text-04 text-gray]
[`www.google.com/maps/d/viewer`](https://www.google.com/maps/d/viewer?mid=1El0Gzo-efzH7pBkaFT8nHMwRiVR-1JFI&ll=25.39827248419623%2C156.78839700294202&z=2)
@snapend

Note:
* Last year,... I was challenged to talk or poster at Python Conference around the world, which I called PyCon tour.
* I presented at 9 conferences on the tour, mostly in Asia.
* This talk could be the final point of the tour, so I'm deeply moved.
* Now, let's get back to the main topic.

---

## Background and Motivation

Note:
(2m)
* First, I will talk about the Background and Motivation of this talk.

+++

### Conference Tasks

* I held PyCon JP(2014-2016) as @color[SeaGreen](Chair)
* Conference tasks:
  * 👨‍💻 Keynotes, Talks and Trainings arrangement
  * 🎫 Ticket sales and reception
  * 🏬 Venue and facility(WiFi, Video...) management
  * 🍱 Foods, ☕️ Coffee, 🧁 Snacks and 🍺 Beers

Note:

* I held PyCon JP event several years in the past.
* As you can imagine, lots of tasks to hold Conference.
* For example, talk arrangements, ticket sales, venue management, food...
* And, ...

+++

### Staff ask me the same things

* 40+ staff
* 🐣 NEW staff : 🐔 OLD staff = 50 : 50

Note:

* The number of PyCon JP staff is 40 over, half of them are the new staff.
* New staff ask similar things to me. And I send similar answers repeatedly.
* But, ...

+++

## Programmer is Lazy

Note:

* As you know, programmers dislike routine work. I also dislike it VERY much.

+++

## Let's create a secretary!!

Note:

* I want someone to do my bothersome tasks instead of me like a secretary.
* Let's make it.

---

## Goal

* How to create @color[SeaGreen](Simple) bot
* How to create @color[SeaGreen](Interactive) bot
* How to @color[SeaGreen](Extend) bot using libs and APIs

Note:
(1m)
* The goal of this talk.
* You'll learn how to create simple bot,
* how to create interactive bot,
* how to extend bot using libraries and APIs through various case studies.
* Then you'll be able to automate your boring stuff with Slackbot!!

---

## Why Slackbot

* Slack running all the time on 💻 📱
* Easy to access Slack
* To do @color[SeaGreen](Everything) in Slack

![slack](20190224pyconapac/images/slack.png)
	
Note:
(1m)

* My secretary is chatbot for Slack.
  * Do you know Slack? Slack is a instant messaging platform.
* I have Slack running all the time on my PC and smartphone.
* This makes it easy to access Slack. I want to do everything in Slack.
* Let's make a chatbot for Slack.

---

## Simple integration with Incoming Webhooks

Note:
(5m)

* First, I will explain Simple integration with Incoming Webhooks.

+++

### System overview

![Overview of Incoming Webhook](20190224pyconapac/images/webhook-overview.png)

Note:

* This is system overview of Incoming Webhooks.
* When program send a message to a Webhook URL via HTTPS, the message will send to Slack.

+++

### Create Incoming Webhooks Integration

* Generate @color[SeaGreen](Webhook URL)
  1. Create a Slack app
  2. Enable Incoming Webhooks in the app
  3. Create an Incoming Webhook
* Webhook URL:

```
https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX
```

* see: [Incoming Webhooks](https://api.slack.com/incoming-webhooks)

Note:

* How to generate Webhook URL is as follows....

+++?image=20190917pyconjp/images/create-app1.png&size=70% auto

Note:
* Create a Slack app

+++?image=20190917pyconjp/images/create-app2.png&size=auto 70%

Note:
* Create a Slack app

+++?image=20190917pyconjp/images/create-app3.png&size=70% auto

@snap[south text-04 text-gray]
* credit: Icons made by [Freepik](https://www.flaticon.com/authors/freepik) from [`www.flaticon.com`](https://www.flaticon.com/)
@snapend

Note:
* Set app icon(option)

+++?image=20190917pyconjp/images/enable-webhook1.png&size=auto 70%

Note:
* Enable webhook

+++?image=20190917pyconjp/images/enable-webhook2.png&size=auto 75%

Note:
* Enable webhook

+++?image=20190917pyconjp/images/create-webhook.png&size=auto 70%

Note:
* Create webhook in your workspace

+++?image=20190917pyconjp/images/get-webhookurl.png&size=auto 70%

Note:
* At last, we got a webhook URL
* OK, We have a webhook URL. Let's send a message to slack with it.

+++

### message with cURL

```bash
$ curl -X POST -H 'Content-type: application/json' \
> --data '{"text": "Hello Slack"}' \
> https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXX
```

![Hello Slack from cURL](20190917pyconjp/images/webhook-curl.png)

Note:

* We send a simple message with cURL.
* When we send a message with JSON, the message will be displayed in Slack.

+++

### message with Python

```python
import json
from urllib import request

URL = 'https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXX'
data = {'text': 'Hello from Python!'}
jsoned = json.dumps(data)
req = request.Request(URL, data=jsoned, method='POST')
request.urlopen(req)
```

![Hello from Python!](20190917pyconjp/images/webhook-python.png)

Note:

* But we are pythonista.
* We use `urllib.requests` module.

+++

### message with Requests

```python
import requests

URL = 'https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXX'
data = {'text': 'Hello from Requests!'}
requests.post(URL, json=data)
```

![Hello from Requests!](20190917pyconjp/images/webhook-requests.png)

Note:

* If you like Requests, it's easy.

+++

### Complex message with Requests

```python
fields = [{'title': 'Love', 'value': 'Ferrets, :beer:, LEGO', 'short': True},
          {'title': 'From', 'value': 'Japan :jp:', 'short': True}]
data = {'attachments': [{
    'pretext': 'Nice to meet you!!',
    'author_name': 'Takanori Suzuki',
    'author_link': 'https://twitter.com/takanory/',
    'text': '*THANK YOU* for coming to my talk !:tada: Please give me *feedback* about this talk :bow:',
    'fields': fields}]}
requests.post(URL, json=data)
```

![Message Attachments](20190917pyconjp/images/webhook-attachments.png)

Note:
We can send complex messages like this with message attachments.

+++

### More complex message

* Block-Kit: new UI framework
* [Introducing Block Kit](https://api.slack.com/block-kit)
* [Block Kit Builder](https://api.slack.com/tools/block-kit-builder)

Note:

* If you need more complex message, you can use Block-Kit.
* Block-Kit is a new UI framework on Slack.
* And Block Kit Builder is interactive prototype builder.

+++?image=20200417pycon/images/block-kit-builder.png&size=contain

+++

```python
import requests

URL = 'https://hooks.slack.com/services/T0XXXXXX/YYYYYYYY/ZZZZZZZ'

places = [{
    'name': 'Masthead Brewing Co',
    'date': 'May 1, 2019',
    'address': '1261 Superior Ave E, Cleveland, OH',
    'tweet': 'https://twitter.com/takanory/status/1123746614768820224',
    'image': 'https://pbs.twimg.com/media/D5hZl0UWsAE8ipN?format=jpg',
    'beers': ['Tire Swing', 'Brute Force Double IPA'],
},
{
    'name': 'Southern Tier Brewery Cleveland',
    'date': 'May 2, 2019',
    'address': '811 Prospect Ave E, Cleveland, OH',
    'tweet': 'https://twitter.com/takanory/status/1124112560058503168',
    'image': 'https://pbs.twimg.com/media/D5mmap5X4AA7kw2?format=jpg',
    'beers': ['8 Days A Week', 'Nu Juice IPA'],
},
{
    'name': 'Punch Bowl Social',
    'date': 'May 3, 2019',
    'address': '1086 W 11th Pl, Cleveland, OH',
    'tweet': 'https://twitter.com/takanory/status/1124459741537865728',
    'image': 'https://pbs.twimg.com/media/D5rvkCzW0AAWTSV?format=jpg',
    'beers': ['Columbus IPA', 'Cloud Cutter Hoppy Wheat Ale',
              'Burning River Pale Ale', 'Elvis Juice', 'Nano OG Lager'],
},
{
    'name': 'Noble Beast Brewing',
    'date': 'May 5, 2019',
    'address': '1470 Lakeside Ave E (E. 13th St.), Cleveland, OH ',
    'tweet': 'https://twitter.com/takanory/status/1125219552781045760',
    'image': 'https://pbs.twimg.com/media/D52VOHEX4AAPAMr?format=jpg',
    'beers': ['[Winter] Evil Motives', 'Sweet Amarillo'],
},
{
    'name': 'Great Lakes Brewing Company',
    'date': 'May 7, 2019',
    'address': 'Concourse C (at CLE Airport), Cleveland, OH',
    'tweet': 'https://twitter.com/takanory/status/1125720508161503233',
    'image': 'https://pbs.twimg.com/media/D59c1jTWAAE-Br2?format=jpg',
    'beers': ['Dortmunder', 'Eliot Ness'],
},
{
    'name': 'Goose Island Beer Company',
    'date': 'May 7, 2019',
    'address': 'Terminal 1, near Gate C10 (ORD Airport), Chicago, IL',
    'tweet': 'https://twitter.com/takanory/status/1125777013330063362',
    'image': 'https://pbs.twimg.com/media/D5-QNopW0AAGl6L?format=jpg',
    'beers': ['Green Line Pale Ale'],
},
]
```

+++

```python
data = {'text': ''}
blocks = []
title = {
    'type': 'section',
    'text': {
        'type': 'mrkdwn',
        'text': ':beer: Beer memories from PyCon 2019',
    }
}
blocks.append(title)  # add title
blocks.append({'type': 'divider'})  # add divider
```

+++

```
for place in places:  # create all place info
    s = {'type': 'section'}
    tweet = f"<{place['tweet']}|Tweet>"
    beers = ', '.join(place['beers'])
    s['text'] = {
        'type': 'mrkdwn',
        'text': f"*{place['name']}* (tweet)\n:beers:: {beers}",
    }
    s['fields'] = [  # fields
        {'type': 'mrkdwn', 'text': f"*Date*: {place['date']}"},
        {'type': 'mrkdwn', 'text': f"*Address*: {place['address']}"},
    ]
    s['accessory'] = {  # image
        'type': 'image',
        'image_url': food['image'],
        'alt_text': food['name'],
    }
    blocks.append(s)

data['blocks'] = blocks
r = requests.post(URL, json=data)
```

+++?image=20200417pycon/images/beermemories.png&size=auto 90%

+++

### Summary of Incoming Webhooks

* @color[SeaGreen](Easy) to send messages from programs ⚙️
* Create @color[SeaGreen](Complex) messages 🛠
* But @color[SeaGreen](One way)(program 👉 Webhook 👉 Slack)

Note:
I want to interact with bot.
Next, I will explain...how to create interactive bot.

---

## Interactive bot with slackbot library

Note:
* Next, I will explain...how to create interactive bot with slackbot library.


+++

### System overview

![Overview of Slackbot](20190224pyconapac/images/slackbot-overview.png)

+++

### Create bot user on Slack

* Create @color[SeaGreen](bot user) 🤖
  1. Create a Slack app
  2. Enable Bots
  3. Add a "Bot User"
  4. Install App to Workspace -> Authorize
* "Bot User OAuth Access Token": `xoxb-123467890-XXXXXX-XXXXXXXXXXXX`
* Invite Bot User to Slack channels

* see: [Creating a bot user](https://api.slack.com/bot-users#creating-bot-user)

Note:
* I describe how to create interactive bot.
* At first, we craete bot user on Slack.

+++?image=20190917pyconjp/images/enable-bots.png&size=auto 70%

Note:
* Enable bots in your app

+++?image=20190917pyconjp/images/add-bot1.png&size=70% auto

Note:
* Add a Bot user

+++?image=20190917pyconjp/images/add-bot2.png&size=auto 70%

Note:
* Add a Bot user

+++?image=20190917pyconjp/images/reinstall-app.png&size=auto 70%

Note:
* Re-install app in your workspace

+++?image=20190917pyconjp/images/get-bot-token.png&size=70% auto

Note:
* We got a Access Token

+++?image=20190917pyconjp/images/invite-bot.png&size=70% auto

Note:
* At last, invite Bot to channels

+++

### slackbot library

* A simple chat bot for Slack
* Python 3.4+
* [`github.com/lins05/slackbot`](https://github.com/lins05/slackbot)
* `pip install slackbot`

Note:
* Then, I will create my bot program with slackbot library
* slackbot is a chat bot framework for Python

+++

### Install slackbot with venv

```shell
$ mkdir beerbot
$ cd beerbot
$ python3.7 -m venv env
$ . env/bin/activate
(env) $ pip install slackbot
```

Note:
* I make venv and install slackbot library for my bot project.
* Then, I make simplest slackbot with 4 files.

+++

### Create a simple bot with slackbot

* `slackbot_settings.py`

```python
API_TOKEN = "xoxb-123467890-XXXXXX-XXXXXXXXXXXXX"  # Bot token
PLUGINS = ['beerbot.plugins']  # Plugin packages
```

* `run.py`

```python
from slackbot.bot import Bot

def main():
    bot = Bot()
    bot.run()

if __name__ == "__main__":
    main()
```

Note:

+++

### Simple Plugin

* `beerbot/plugins/__init__.py`

```shell
(env) $ mkdir -p beerbot/plugins
(env) $ touch beerbot/plugins/__init__.py  # empty file
```

* `beerbot/plugins/sample.py`

```python
from slackbot.bot import listen_to

@listen_to('Hi')
def hello(message):
    message.send('Hi!!! I am beerbot! :beer:')
```

Note:

* That's all.

+++

### File structure

```
.
├── beerbot
│   └── plugins
│       ├── __init__.py
│       └── sample.py
├── run.py
└── slackbot_settings.py
```

Note:
* File structure is here
 
+++

### Run slackbot

* `(env) $ python run.py`

![First Slackbot](20190917pyconjp/images/slackbot-hi.png)

Note:

* Let's run the bot.
* I guess you understood the basic way to make Slackbot, so we will extend it.

---

## Extend slackbot

+++

### decorator

* `listen_to`: message sent on @color[SeaGreen](a channel)
* `respond_to`: message sent to @color[SeaGreen](the bot)

```python
from slackbot.bot import listen_to, respond_to

@listen_to('Hi')
def hello(message):
    message.send('Hi!!! I am beerbot! :beer:')

@respond_to('cheers')  # mention
def ping(message):
    message.send('Cheers! :beers:')
```

Note:
* `listen_to` is called when a message matching the pattern is sent on a channel
* `respond_to` is sent to the bot

+++?image=20190917pyconjp/images/slackbot-decolator.png&size=auto 80%

Note:
* The `cheers` message only works with mention.

+++

### mention

* `message.reply()`

```python
@listen_to('morning')
def morning(message):
    message.reply('Good morning!')  # reply to me
```

![mention](20190922pycontw/images/slackbot-reply.png)

+++

### emoji reaction

* `message.react()`

```python
@listen_to('beer')
def hungry(message):
    message.react('beer')  # react beer emoji
```

![react](20200417pycon/images/slackbot-react.png)

+++

### Extract parameters on message

* Use regular expressions

```python
@respond_to('choice (.*)')  # choice pizza beer sushi
def choice(message, words):  # -> words='pizza beer sushi'
    word = random.choice(words.split())
    message.send('I chose *{}*'.format(word))
```

![choice](20190922pycontw/images/slackbot-choice.png)

Note:
* slackbot can handle parameters.
* We use regular expressions with parentheses, it is passed as parameter values.

+++

```python
@listen_to('(\d+)\s*beers')  # 3 beers, 100beers
def bees(message, num):  # num='3' or '100'
    beers = ':beer:' * int(num)
    if beers:
        message.send(beers)
```

![beers](20190922pycontw/images/slackbot-beers.png)

+++

### `slackbot_settings.py`

```python
ALIASES = '$'  # Prefix instead of mention (@mybot ping -> $ping)
ERRORS_TO = 'mybot-error'  # Error reporting channel
DEFAULT_REPLY = "Sorry but I didn't understand you"
PLUGIN = ['mybot.plugins', 'other.plugins',]  # Pluing packages
```

![Settings](20190917pyconjp/images/slackbot-settings.png)

Note:
Slackbot has several settings.

+++

### Attachments support

```python
import json

@respond_to('follow me')
def followme(message):
    attachments = [{
        'author_name': 'Takanori Suzuki',
        'text': 'Follow me! <https://twitter.com/takanory|@takanory>',
        'color': '#59afe1'
    }]
    message.send_webapi('', json.dumps(attachments))
```

![Attachments](20190917pyconjp/images/slackbot-attachments.png)

+++

### Summary of Slackbot

* We can @color[SeaGreen](communicate) with Slackbot
* Slackbot can handle @color[SeaGreen](parameters) in messages
* Slackbot can send messages in @color[SeaGreen](various formats)

Note:
I think you understood Slackbot can do various things.
Next,...

---

## Case studies

Note:
I will show you some case studies combining Python libraries and APIs.

---

## Calculator function using SymPy

+++

### Calculator function using SymPy

* Motivation
  * I feel heavy to call a calculator app on my smartphone
  * It seems useful if @color[SeaGreen](Slack as a calculator)

+++

### about SymPy

* SymPy: Python library for symbolic mathematics
  * [`www.sympy.org`](https://www.sympy.org/)
* `$ pip install sympy`

+++

* `calc.py`

```python
from slackbot.bot import listen_to
from sympy import sympify, SympifyError

@listen_to(r'^([-+*/^%!().\d\s]+)$')  # Formula like pattern
def calc(message, formula):
    try:
        result = sympify(formula)  # Simplifies the formula
        if result.is_Integer:
            answer = int(result)  # Convert to interger value
        else:
            answer = float(result)  # Convert to float value
        message.send(f'{answer:,}')
    except SympifyError:
        pass
```

+++?image=20190917pyconjp/images/slackbot-calc.png&size=auto 80%

---

## Plusplus function using Peewee ORM

+++

### Plusplus function using Peewee ORM

* Motivation
  * In PyCon JP, I want to make a culture that @color[SeaGreen](appreciates) each other staff 👍

+++

### about Peewee

* Simple and small @color[SeaGreen](ORM).
  * a small, expressive ORM
  * python 2.7+ and 3.4+ (developed with 3.6)
  * supports sqlite, mysql and postgresql
* [`docs.peewee-orm.com`](http://docs.peewee-orm.com/en/latest/)
* `$ pip install peewee`

+++

### `plusplus_model.py`

```python
from pathlib import Path
from peewee import SqliteDatabase, Model, CharField, IntegerField

dbpath = Path(__file__).parent / 'plusplus.db'  # db file
db = SqliteDatabase(dbpath)

class Plusplus(Model):
    name = CharField(primary_key=True)  # fields
    counter = IntegerField(default=0)

    class Meta:
        database = db

db.connect()
db.create_tables([Plusplus], safe=True)
```

+++

### `plusplus.py`

```
from slackbot.bot import listen_to

from .plusplus_model import Plusplus

@listen_to(r'^(\w+)\+\+')
def plusplus(message, name):
    target = name.lower()
    # Get or create object
    plus, created = Plusplus.get_or_create(
        name=target, defaults={'counter': 0})
    plus.counter += 1
    plus.save()
    message.send(f'Thank you {name}! (count: {plus.counter})')
```

+++?image=20190917pyconjp/images/slackbot-plusplus.png&size=auto 80%

---

## Display JIRA issue and Search issues

+++

### Display JIRA issue and Search issues

* Motivation
  * JIRA is very useful
  * JIRA Web is @color[SeaGreen](very heavy)
  * I want to check issue details @color[SeaGreen](without JIRA Web)

+++

### System Overview

![Overview of JIRA](20190224pyconapac/images/jira-overview.png)

+++

### about Python JIRA

* Python library to work with JIRA APIs
* [`jira.readthedocs.io`](https://jira.readthedocs.io/)
* `$ pip install jira`			

+++

### Authentication

```python
from jira import JIRA

URL = 'https://jira.atlassian.com/'
jira = JIRA(URL, basic_auth=('user', 'pass'))
```

* see: [2.1.2. Authentication](https://jira.readthedocs.io/en/master/examples.html#authentication)

+++

### Get Issue object

```python
@listen_to(r'(ISSHA-[\d]+)')  # Issue id pattern
def jira_issue(message, issue_id):
    issue = jira.issue(issue_id)
    summary = issue.fields.summary
    status = issue.fields.status.name
    assignee = issue.fields.assignee.name
    issue_url = issue.permalink()
    attachments = [{
        'pretext': f'<{issue_url}|{issue_id}> {summary}',
        'fields': [{'title': 'Assignee', 'value': assignee},
                   {'title': 'Status', 'value': status}],
    }]
    message.send_webapi('', json.dumps(attachments))
```

* see: [2.1.3 Issues](https://jira.readthedocs.io/en/master/examples.html#issues)

+++

![JIRA issue](20190224pyconapac/images/slackbot-jira-issue.png)

+++

### Search issues

```python
@respond_to('jira (.*)')
def jira_search(message, keywords):
    # make JQL query string
    jql = f'project=ISSHA and text ~ "{keywords}" order by created desc'
    text = ''
    # get 5 recent issues
    for issue in jira.search_issues(jql, maxResults=5):
        id = issue.key
        url = issue.permalink()
        summary = issue.fields.summary
        text += f'- <{url}|{id}> {summary}\n'
    message.send(text)
```

* see: [2.1.5 Searching](https://jira.readthedocs.io/en/master/examples.html#searching)
* JQL: JIRA Query Language
* see: [Advanced searching - Atlassian Documentation](https://confluence.atlassian.com/jiracoreserver073/advanced-searching-861257209.html)

+++

![JIRA search](20190224pyconapac/images/slackbot-jira-search.png)

---

## Create multiple issues from a template

+++

### Create multiple issues from a template

* Motivation
  * In pycamp event, **20+ issues** are required for each event
  * Copying issues @color[SeaGreen](by hand is painful)
  * JIRA Web is @color[SeaGreen](very Heavy) (again)

Note:
* PyCon JP hold pycamp every month.

+++

### System Overview

![Overview of template](20190224pyconapac/images/template-overview.png)

+++

### Google Authorization is VERY Complex(1/2)

* create Google Cloud Platform project
  * enable API(in this case: Google Sheets API)
  * download `credentials.json`
* Install Google Client Library
  * `pip install google-api-python-client google-auth-oauthlib`

Note:
* At firest, we make Google Authorized token.

+++

### Google Authorization is VERY Complex(2/2)

* download [`quickstart.py`](https://github.com/gsuitedevs/python-samples/blob/master/sheets/quickstart/quickstart.py) on GitHub
* run `quickstart.py`
  * select your Google account in Web browser
  * Click the Accept button
  * get `token.pickle` file(finish!!)

```shell
(env) $ python quickstart.py
Please visit this URL to authorize this application: https://accounts.google.com/o/oauth2/auth?response_type=code&.....
Name, Major:
Alexandra, English
:
```

* see: [Python Quickstart | Sheets API | Google Developers](https://developers.google.com/sheets/api/quickstart/python)

Note:

* But, if we can use Google's API, we can do many things

+++

### Get Spreadsheet Data

```python
from googleapiclient.discovery import build
SHEET_ID = '1LEtpNewhAFSXXXXXXXXXXXXX'

creds = None
if os.path.exists('token.pickle'):
    with open('token.pickle', 'rb') as token:
        creds = pickle.load(token)
# build service
service = build('sheets', 'v4', credentials=creds)
# get data from Spreadsheet
result = service.spreadsheets().values().get(
    spreadsheetId=SHEET_ID, range='sheet_name!A:G').execute()
for row in result.get('value', []):
    print(row[0], row[1])  # Cell A and B
```

* see: [Method: spreadsheets.values.get](https://developers.google.com/sheets/api/reference/rest/v4/spreadsheets.values/get)

+++

### Create JIRA Issue

```python
duedate = datetime.date.today + datetime.timedelta(days + 14)
issue_dict = {
    'project': {'key': PROJECT},
    'components': [{'name': COMPONENT}],
    'summary': SUMMARY_TEXT,
    'description': LONG_DESCRIPTION,
    'assignee': {'name': NAME_OF_ASSIGNEE},
    'reporter': {'name': NAME_OF_REPORTER},
    'duedate': f'{duedate:%Y-%m-%d}'
}
issue = jira.create_issue(fields=issue_dict)  # create issue
```

* see: [2.1.3 Issues](https://jira.readthedocs.io/en/master/examples.html#issues)

+++

### Sample of template command

* `$pycamp create`: Create issues for pycamp event

![Sample of Template command](20190224pyconapac/images/template-bot-sample.png)

+++?image=20190224pyconapac/images/template-pycamp-template.png&size=auto 90%

Note:

* Here is the pycamp issue template.

+++?image=20190224pyconapac/images/template-created-issues.png&size=auto 90%

Note:

* As you can see, I can create many tickets for pycamp in one command.
* I am very happy.

+++

### Source code of pycamp command

* see: [`github.com/pyconjp/pyconjpbot/blob/master/pyconjpbot/plugins/pycamp.py`](https://github.com/pyconjp/pyconjpbot/blob/master/pyconjpbot/plugins/pycamp.py)

+++

### I never have to copy issues again 🎉

---

## Account management of G Suite

+++

### Account management of G Suite

* Motivation
  * PyCon JP use `pycon.jp` domain with G Suite
  * I only use Google Admin web occasionally
  * @color[SeaGreen](I forgot) to use admin screen

Note:

* create a new staff account
* add email address to groups

+++

### System Overview

![Overview of gadmin](20190224pyconapac/images/gadmin-overview.png)

+++

### Update Google Authorization

* update Google Cloud Platform project
  * add G Suite Admin API
  * re-download `credentials.json`
* re-run `quickstart.py`
  * get new `token.pickle`

```shell
(env) $ python quickstart.py
Please visit this URL to authorize this application: https://accounts.google.com/o/oauth2/auth?response_type=code&.....
Name, Major:
Alexandra, English
:
```

Note:

* If we use the new API we need to re-authenticate

+++

### Get user list

```python
# build service
DOMAIN = 'pycon.jp'
service = build('admin', 'directory_v1', credentials=creds)

# get user list
users_list = service.users().list(orderBy='email', domain=DOMAIN).execute()
for user in users_list.get('users', []):
    email = user['primaryEmail']
    fullname = user['name']['fullName']
    print(f'{email} {fullname}')
```

* see: [Users: list | Directory API](https://developers.google.com/admin-sdk/directory/v1/reference/users/list)

+++

### Insert user

```python
body = {
    'primaryEmail': EMAIL_ADDRESS,
    'password': PASSWORD,
    'name': {
        'givenName': FIRST_NAME,
        'familyName': LAST_NAME,
    },
}
try:
    service.users().insert(body=body).execute()
except:
    pass  # fail
```

* see: [Users: insert | Directory API](https://developers.google.com/admin-sdk/directory/v1/reference/users/insert)

+++

### Suspend, Resume, Delete user

```python
suspend = {'suspended': True}
service.users().update(userKey=EMAIL, body=suspend).execute()

resume = {'suspended': False}
service.users().update(userKey=EMAIL, body=resume).execute()

service.users().delete(userKey=email).execute()
```

* see: [Users: update | Directory API](https://developers.google.com/admin-sdk/directory/v1/reference/users/update)
* see: [Users: delete | Directory API](https://developers.google.com/admin-sdk/directory/v1/reference/users/delete)

+++?image=20190224pyconapac/images/gadmin-help.png&size=auto 90%

+++?image=20190224pyconapac/images/gadmin-user-list.png&size=auto 90%

+++?image=20190224pyconapac/images/gadmin-member-list.png&size=auto 90%

+++

### I can completely forget Google Admin 🎉 🎉

+++

### Source code of gadmin command

* see: [`github.com/pyconjp/pyconjpbot/blob/master/pyconjpbot/google_plugins/gadmin.py`](https://github.com/pyconjp/pyconjpbot/blob/master/pyconjpbot/google_plugins/gadmin.py)

---

## Summary

* Simple bot with Incoming Webhooks
* Interactive bot with `slackbot`
* `slackbot` with libraries and apis

Note:
* You'be learned how to create simple bot with incoming webhooks,
* how to create interactive bot with slackbot,
* how to extend slackbot with libraries and APIs.

+++

## Next steps

* Let's make @color[SeaGreen](your own bot)
* Let's use libraries and APIs in your bot
* Automate your Boring Stuff with Slackbot

Note:
* Then you will have more free time, so you can do more creative things!!

+++

![Thank you!!](20200417pycon/images/slackbot-trans.png)

* @fab[twitter] [@takanory](https://twitter.com/takanory)
* @fab[github] [`github.com/takanory/slides`](https://github.com/takanory/slides)

+++

### `$trans` command

* `pip install googletrans`

```python
from googletrans import Translator
from slackbot.bot import respond_to

@respond_to('^trans\s+(.+)\s+([\w-]+)$')
def trans(message, text, dest):
    translator = Translator()
    t = translator.translate(text, dest=dest)
    message.send(t.text)
```

+++

![Thank you!!](20200417pycon/images/slackbot-trans.png)

* @fab[twitter] [@takanory](https://twitter.com/takanory)
* @fab[github] [`github.com/takanory/slides`](https://github.com/takanory/slides)