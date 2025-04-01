# ScrapeMeQuickly

Welcome to the ScrapeMeQuickly hackathon challange


### Example with scraping run id of 89d5dca4-0a34-11f0-b686-4a33b21d14f6
```json
{
    "min_year": 1934,
    "max_year": 2024,
    "avg_price": 24148,
    "mode_make": "Volkswagen Passat B3"
}
```

### Create a team
```python
def create_team(team_name: str, team_email: str) -> str:
    r = requests.post(
        "https://api.scrapemequickly.com/register",
        data=json.dumps({"team_name": team_name, "team_email": team_email}),
        headers={"Content-Type": "application/json"}
    )

    if r.status_code != 200:
        print(r.json())
        print("Failed to start scraping run")
        sys.exit(1)

    return r.json()["data"]["team_id"]
```

### Start a scraping run
```python
def start_scraping_run(team_id: str) -> str:
    r = requests.post(f"https://api.scrapemequickly.com/scraping-run?team_id={team_id}")

    if r.status_code != 200:
        print(r.json())
        print("Failed to start scraping run")
        sys.exit(1)

    return r.json()["data"]["scraping_run_id"]
```

### Submit your answers
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
