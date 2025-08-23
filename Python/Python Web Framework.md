## Django and Flask


Flask 
1. pip install Flask
2. Setup virtual env (contained space for project dependencies)
   python -m venv venv_name
3. Activate virtual env - source venv/bin/activate
app.py
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
   return 'Hello, Flask'


if __name__ == '__main__':
   app.run(debug=True)
```

flask run --debug to start the server


ORM 

Flask-SQLAlchemy

pip install Flask-SQLAlchemy

pip install Flask-Migrate help us to easily update schema as our application evolves



