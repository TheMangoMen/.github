# MangoMen

# Live Code

Frontend: [https://mango-helguind.csclub.cloud/](https://mango-helguind.csclub.cloud/)

Backend: [https://mango-api-helguind.csclub.cloud/](https://mango-api-helguind.csclub.cloud/)

# Creating the DB and Populating

Our dataset was extracted as a csv file. We have an endpoint set up on our backend server to create the database and populate it using the csv file.

```python
@app.get("/hevy/create")
async def create_hevy_db():
    cur.execute(f"""
        CREATE TABLE IF NOT EXISTS {HEVY_TABLE} (
            title VARCHAR(255),
            start_time TIMESTAMP,
            end_time TIMESTAMP,
            description TEXT,
            exercise_title VARCHAR(255),
            superset_id INT,
            exercise_notes TEXT,
            set_index INT,
            set_type VARCHAR(50),
            weight_lbs DECIMAL,
            reps INT,
            distance_km DECIMAL,
            duration_seconds INT,
            rpe INT
        );

        COPY {HEVY_TABLE} FROM '{HEVY_DATA_PATH}' WITH CSV HEADER;
    """)
```

# Fetching Data

```python
@app.get("/hevy/titles")
async def get_hevy_titles():
    cur.execute(f"SELECT DISTINCT title FROM {HEVY_TABLE};")
    records = cur.fetchall()
    return [i[0] for i in records]

@app.get("/hevy/workouts")
async def get_hevy_workouts():
    cur.execute(f"SELECT * FROM {HEVY_TABLE} LIMIT {MAX_ROWS};")
    records = cur.fetchall()
    return records

@app.get("/hevy/workouts/{title}")
async def get_hevy_workouts_by_title(title):
    cur.execute(f"SELECT * FROM {HEVY_TABLE} WHERE title='{title}' LIMIT {MAX_ROWS};")
    records = cur.fetchall()
    return records
```

# Setup

## Install and Start Postgres

```bash
brew install postgres
brew services start postgresql
```

## Create a Database

```bash
createdb milestone0
psql -d milestone0
```

## Run the Backend

In the `backend` repo, run

```bash
pip install -r requirements.txt
fastapi dev main.py
```
