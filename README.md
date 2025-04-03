# ScrapeMeQuickly

Welcome to the [Scrape Me Quickly](https://scrapemequickly.com) hackathon challange by Ping Proxies

The goal is to collect information about all of the cars on [the site](https://scrapemequickly.com/cars/static/0?scraping_run_id=89d5dca4-0a34-11f0-b686-4a33b21d14f6), as quickly as possible.

(Example Seed: DO NOT USE this Scraping Run ID)

For any page that you are collecting data from, it is important that you **Attach your Scraping Run ID** in the query string as shown below.
`?scraping_run_id={scraping-run-id}`

You must submit: minimum year, maximum year, average price and mode (most common) make.

### Requirements
```python
import requests
import sys
import json
```

### [Create a team](https://scrapemequickly.com/team)
```python
def create_team(team_name: str, team_email: str) -> str:
    r = requests.post(
        "https://api.scrapemequickly.com/register",
        data=json.dumps({"team_name": team_name, "team_email": team_email}),
        headers={"Content-Type": "application/json"}
    )

    if r.status_code != 200:
        print(r.json())
        print("Failed to create a team")
        sys.exit(1)

    return r.json()["data"]["team_id"]
```

### [Start a scraping run](https://scrapemequickly.com/start)
```python
def start_scraping_run(team_id: str) -> str:
    r = requests.post(f"https://api.scrapemequickly.com/scraping-run?team_id={team_id}")

    if r.status_code != 200:
        print(r.json())
        print("Failed to start scraping run")
        sys.exit(1)

    return r.json()["data"]["scraping_run_id"]
```

### [Submit your answers](https://scrapemequickly.com/submit)
```python
def submit(answers: dict, scraping_run_id: str) -> bool:
    r = requests.post(
        f"https://api.scrapemequickly.com/cars/solve?scraping_run_id={scraping_run_id}",
        data=json.dumps(answers),
        headers={"Content-Type": "application/json"}
    )

    if r.status_code != 200:
        print(r.json())
        print("Failed to submit answers")
        return False

    return True
```
#### Example with scraping run id of 89d5dca4-0a34-11f0-b686-4a33b21d14f6
```json
{
    "min_year": 1934,
    "max_year": 2024,
    "avg_price": 24148,
    "mode_make": "volkswagen"
}
```


### FAQ's
- What is a **Team ID**?
A Team ID is the ID we have generated for your given team with the team name that you provided.

- What is a **Scraping Run**?
A scraping run is a 'time trial' of your scraping, started at time of creation and ended when the answer has been submitted. A Team ID is required to start a new scraping run.

- What is a **Scraping Run ID**?
A scraping run ID is the ID that we have generated for a Scraping Run.

- Why can I not submit another answer for my current scraping run?
Only one answer submission can be made per scraping run, you must create a new one to try again.

- How come I have sumbitted the correct answer but it was rejected?
Please ensure your results are sent in the requested format. If you are still unsure, visit us at the event.

- I am being rate-limited, what do I do?
Use the list of proxies provided to help with this.

- What languages can I use?
Any programming language can be used as long as the answers are submitted to the API endpoint correctly.

- Can I have a hint?
The first hint is available on https://scrapemequickly.com

- Can I have a job?
We are currently hiring! Visit https://careers.pingproxies.com/jobs for more info.
