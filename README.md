# House Price Predictor — ML Model Deployment

A hands-on workshop that walks through the full lifecycle of a machine-learning model: training, serialization, and deployment through three different interfaces (REST API, Python client, and a Flask web application).

![house-predictor](house_predictor.png)

---

## What this repository does

This project demonstrates how to build and deploy a scikit-learn **Linear Regression** model that predicts house sale prices based on property characteristics. It covers four deployment stages:

| Stage | File | Description |
|-------|------|-------------|
| 1 – Training | `homework/train_model.py` | Trains the model on `house_data.csv` and serializes it to `house_predictor.pkl` |
| 2 – REST API | `homework/api_server.py` | Flask server that accepts a JSON POST request and returns the predicted price |
| 3 – API Client | `homework/api_client.py` | Python script that queries the REST API programmatically |
| 4 – Web App | `homework/web_app.py` | Flask web application with a browser-based form for end-user interaction |

### Input features used by the model

- `bedrooms` — number of bedrooms
- `bathrooms` — number of bathrooms
- `sqft_living` — interior living area (sq ft)
- `sqft_lot` — lot size (sq ft)
- `floors` — number of floors
- `waterfront` — waterfront view flag (0/1)
- `condition` — overall condition rating (1–5)

---

## Project structure

```
.
├── files/
│   └── input/
│       └── house_data.csv       # Training dataset
├── homework/
│   ├── api_client.py            # Python REST client
│   ├── api_server.py            # Flask REST API server
│   ├── descriptivo.ipynb        # Exploratory data analysis notebook
│   ├── house_predictor.pkl      # Serialized trained model
│   ├── templates/               # HTML templates for the web app
│   ├── train_model.py           # Model training script
│   └── web_app.py               # Flask web application
├── tests/                       # Automated tests (pytest)
├── requirements.txt
├── setup.py
├── setup.sh                     # Setup script (macOS/Linux)
└── setup.bat                    # Setup script (Windows)
```

---

## Prerequisites

- Python 3.8 or higher
- pip

---

## Setup

### macOS and Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
source setup.sh
```

### Windows

```bash
python3 -m venv .venv
.venv\Scripts\activate
setup
```

---

## Usage

### 1 – Train the model

Run this once to generate `homework/house_predictor.pkl`:

```bash
python homework/train_model.py
```

### 2 – Start the REST API server

```bash
python homework/api_server.py
```

The server listens on `http://127.0.0.1:5000`. Send a prediction request with `curl`:

```bash
# macOS / Linux
curl http://127.0.0.1:5000 -X POST \
  -H "Content-Type: application/json" \
  -d '{"bathrooms": "2", "bedrooms": "3", "sqft_living": "1800", \
       "sqft_lot": "2200", "floors": "1", "waterfront": "1", "condition": "3"}'

# Windows
curl http://127.0.0.1:5000 -X POST -H "Content-Type: application/json" \
  -d "{\"bathrooms\": \"2\", \"bedrooms\": \"3\", \"sqft_living\": \"1800\", \"sqft_lot\": \"2200\", \"floors\": \"1\", \"waterfront\": \"1\", \"condition\": \"3\"}"
```

### 3 – Run the Python API client

With the server running, execute:

```bash
python homework/api_client.py
```

### 4 – Launch the web application

```bash
python homework/web_app.py
```

Open your browser at `http://127.0.0.1:5000`, fill in the property details, and click **Predict** to see the estimated price.

---

## Running tests

```bash
pytest
```

---

## Tech stack

| Library | Purpose |
|---------|---------|
| [scikit-learn](https://scikit-learn.org/) | Model training (Linear Regression) |
| [pandas](https://pandas.pydata.org/) | Data loading and feature engineering |
| [Flask](https://flask.palletsprojects.com/) | REST API and web application |
| [requests](https://requests.readthedocs.io/) | HTTP client for the API consumer |
| [pytest](https://pytest.org/) | Automated testing |