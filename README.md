# lukhed_sports
A collection of sports analysis utility functions and API wrappers

```bash
pip install lukhed-sports
```


## Sportspage Feeds Wrapper
This class is a custom wrapper for the [sportspagefeeds API](https://sportspagefeeds.com/documentation). 

It provides:
- Management of api key -> You can store api key locally (by default) or with a private github repo 
    so you can use the api efficiently across different hardware.
- Optionally manage api limits (on by default) 
- Methods to utilize each endpoint from sportspagefeeds
- Optionally validate input (on by default), to ensure you do not waste API calls
- Methods to get valid inputs for each endpoint, as documentation is sparse
- Methods to parse data returned by basic (non-paid) endpoints 

Full documentation for this class is in development.

### Basic Usage
```python
from lukhed-sports import SportsPage
```

#### API Key Management Locally
```python
# Upon first use, class will take you thru setup (copy and paste your Sportspage key)
api = SportsPage()
games = api.get_games('nfl')
```

#### API Key Managment with Private Github Repo
```python
# Upon first use, class will take you thru setup (github token and Sportspage key)
api = SportsPage(
    config_file_preference='github', 
    github_project='any_project_name'
    )
```

#### Games
```python
# Get games occuring today
api.get_games('nfl')
```

Partial example resopnse below, for full example response [see here.]([lukhed_sports/example_responses/nflGames.json](https://github.com/lukhed/lukhed_sports/blob/62abe3400f6abd69b1cf73ea3b97d59ec2ad5a10/lukhed_sports/example_responses/nflGames.json))
```json
{
    "status": 200,
    "time": "2024-12-30T19:11:10.045Z",
    "games": 1,
    "skip": 0,
    "results": [
        {
            "summary": "Detroit Lions @ San Francisco 49ers",
            "details": {
                "league": "NFL",
                "seasonType": "regular",
                "season": 2024,
                "conferenceGame": true,
                "divisionGame": false
            },
    ...
```

#### Rankings
```python
rankings = api.get_rankings('ncaaf')
```

Partial example resopnse below, for full example response [see here.]([tbd](https://github.com/lukhed/lukhed_sports/blob/dae9a5e1b35407c652f78620b44f03a94adf4529/lukhed_sports/example_responses/getRankings.json))
```json
{
    "status": 200,
    "time": "2025-01-05T17:12:24.613Z",
    "results": [
        {
            "name": "College Football Playoff",
            "rankings": [
                {
                    "rank": 1,
                    "team": "Oregon",
                    "teamId": 1388
                },
                {
                    "rank": 2,
                    "team": "Georgia",
                    "teamId": 1365
                },
        ...
```

#### Check API Usage
```python
api.check_api_limit()

# print to console
>>>
You have 4 api calls remaining
Your reset time is set for 20241230194114 US/Eastern
Your limit is 20
```

Response
```json
{
    "limit": 20,
    "remaining": 15,
    "resetTime": "20250105194115",
    "lastCall": "20250105121251"
}
```
