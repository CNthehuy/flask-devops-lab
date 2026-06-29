# Flask DevOps Lab
2nd controlled conflict
## Usage
This is meant to be used as a learning environment to practice the use of Git, GitHub, and Docker. No other use is permitted.

## How to Run on Linux
``` Python
git clone https://github.com/CNthehuy/flask-devops-lab.git
cd flask-devops-lab
source .venv/bin/activate
pip install -r requirements.txt
python app.py
```

1. api/health - checks if Flask application is running and can take requests.
2. api/config - exposes config values or runtime settings.
3. api/report - generates or returns application reports in JSON format.
