# scrapemequickly


```python
def create_team(team_name: str, team_email: str) -> str:
    r = requests.post(
        f"{url}/register", data=json.dumps({"team_name": team_name, "team_email": team_email}), headers={"Content-Type": "application/json"}
    )

    if r.status_code != 200:
        print(r.json())
        print("Failed to start scraping run")
        sys.exit(1)

    return r.json()["data"]["team_id"]
```
