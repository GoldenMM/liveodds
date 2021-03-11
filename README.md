![liveodds](https://i.postimg.cc/fb9KZ044/liveodds-tp.png)

<p align="center">
  <img src="https://i.postimg.cc/6pC44nV9/build-joints-brightgreen.png">
  <img src="https://i.postimg.cc/DmkBxCk0/joint-passing-brightgreen.png">
  <img src="https://i.postimg.cc/3NDtjsqz/checks-bouncing-brightgreen.png">
  <img src="https://i.postimg.cc/0Q4twkVp/comments-0-yellowgreen.png">
</p>


Unofficial (and highly illegal) Python  API for Oddschecker


Plan to cover a few of the main sports but Racing and Football are only guarantees so far. Golf, Tennis, Greyhounds, Basketball, NFL etc could possibly follow if I don't get bored and if there is sufficient interest. Requests in discussions will be considered, briefly at least, and indeed at most.

<br>

#### Table of Contents
- [Requirements](#requirements)
- [Install](#install)
- [Usage](#usage)
- [API](#racing)
    - [Racing](#racing)
        - [Meeting](#meeting)
        - [Race](#race)
        - [Examples](#examples-1)
    - [Football](#racing)
        - [Competition](#competition)
        - [Match](#match)
        - [Examples](#examples-2)
- [Disclaimer](#disclaimer)

<br>

## Requirements
Python 3.6 or greater is needed, you can get the latest version [here](https://www.python.org/downloads/). In addition, the modules [lxml](https://lxml.de/), [requests](https://requests.readthedocs.io/en/master/), [aiohttp](https://docs.aiohttp.org/en/stable/) are needed. They can be installed using PIP(included with Python) with the following command.

` pip3 install lxml requests aiohttp`

<br>

## Install

Clone the repo with [git](https://git-scm.com/downloads)

`git clone https://github.com/4A47/liveodds.git`

or [download](https://github.com/4A47/liveodds/archive/main.zip) the zip.


<br>

## Usage
Documentation is possible in the future, in the meantime, most of the existing functionality will be shown in example files and here.

To use the API, copy the **inner** liveodds folder to your project. 

Only football and racing are confirmed thus far but this will be the style of import for any sport that gets covered.

```python
from liveodds.football import Football
from liveodds.racing import Racing
```

<br>

## Racing
The 2 important classes to know are **Meeting** and **Race**. The main Racing class provides a few methods to assist in accessing Meeting objects, which contain Race objects for each race at the meeting.

<details>
<summary>More info</summary>

#### Racing Class: Methods and Properties

| Methods                                      | Description                                                                          |
|----------------------------------------------|--------------------------------------------------------------------------------------|
| courses(date: str, region: str)              | Returns a list of string course names for a given date and region                    |
| dates()                                      | Returns a list of string dates where races are available                             |
| meeting(date: str, region: str, course: str) | Returns a specific meeting object for a given date, region and course                |
| meetings(date: str, region: str)             | Returns a list of Meeting objects for all meetings on a given date in a given region |
| meetings_dict(date: str, region: str)        | Returns a dict of Meeting objects for all meetings on a given date in a given region |
| regions(date: str)                           | Returns a list of string region codes for a given date                               |


</details>

<br>

#### Meeting

**Meeting objects** are stored in a nested dictionary in the Racing class and can be accessed directly with the underlying Racing._meetings member, and for non lunatics, indirectly, using the convenience methods provided.


#### Racing.meeting(date: str, region: str, course: str)
_Returns a specific meeting object_


#### Racing.meetings(date: str, region: str)
_Returns a list of meeting objects for a given date and region._

<details>
<summary>More info</summary>

#### Meeting class: Methods and Properties

| Methods          | Description                                                          |
|------------------|----------------------------------------------------------------------|
| race(time: str)  | Returns a specific Race object from the meeting for a given off time |
| races()          | Returns a dictionary of all races from the meeting                   |
| times()          | Returns a list of string off times for all races at meeting          |


| Properties       | Description                               |
|------------------|-------------------------------------------|
| date: str        | Date of the race                          |
| region: str      | 2 or 3 letter region code (ALL CAPS)      |
| course: str      | Name of the course                        |

</details>
<br>

### Race

**Race objects** contain the odds and are retrieved using the 
following methods in the Meeting class. 

#### Meeting.race(time: str)
_Returns a specific race object given a start time ie '14:30'_


#### Meeting.races()
Returns a list of race objects for all races in the meeting.

<details>
<summary>More info</summary>

#### Race class: Methods and Properties

| Methods                 | Description                                                                       |
|-------------------------|-----------------------------------------------------------------------------------|
| horses()                | Returns a list of string: horses in the race                                      |
| odds(horse: str = None) | Returns odds dictionary for specific horse if given, otherwise all horses in race |
| json()                  | Returns JSON string of odds for every horses in race                              |
| update_odds()           | Updates the odds of the race                                                      |


| Properties      | Description                                             |
|-----------------|---------------------------------------------------------|
| course :str     | The name of the course                                  |
| date: str       | Date of the meeting                                     |
| region: str     | 2 or 3 letter region code (ALL CAPS)                    |
| time :str       | The off time of the race                                |
| title: str      | The name of the race (Very inconsistent outside UK/IRE) |

</details>
<br>


### Examples

Get race objects for all todays races in the UK

```python
from liveodds.racing import Racing

racing = Racing()

today = racing.dates()[0]

for meeting in racing.meetings(today, 'UK'):
    for race in meeting.races():
        print(race.course, race.time, race.title)
```
<br>

Race objects contain a dictionary where the key is the name of the horse, and the value is a dictionary of bookies odds

```python
courses = racing.courses(today, 'UK')

meeting = racing.meeting(today, 'UK', courses[0])

race_odds = meeting.race(meeting.times()[0]).odds()

for horse in race_odds:
    print(horse, race_odds[horse]['William Hill'])
```
<br>

You can return a JSON string instead of a dictionary with the Race.json() method, and a view of the json should make the structure clear.

```python
race_json = meeting.race(meeting.times()[0]).json()
```

![json](https://i.postimg.cc/CMR4LSMw/json.png)

<br>

## Football


### Competition


### Match


### Examples


<br>


#### Disclaimer
I hereby renounce all liability when the MI6 cybercrime net inevitably closes in on users of this API. If you do, in a moment of misguided recklessness, decide to use this API, you *will* go to jail, no ifs, buts or maybes, the cost of doing business here is hard time. So before you clone, ask yourself just how much you really want access to the latest odds in a python script, and is it worth throwing your life away for it? Would you torrent a car?

