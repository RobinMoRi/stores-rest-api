## Simple REST API project using Python Flask

### Acknowledgements

This project is done along with the Udemy course found on the 
following link:
* [REST API Flask and Python](https://www.udemy.com/course/rest-api-flask-and-python/)

The project is done using:
* Flask
* Flask-JWT
* Flask-RESTful
* SQLAlchemy


### Installation and running API
#### Clone code into local repositories
```bash
git clone https://github.com/RobinMoRi/stores-rest-api.git
cd stores-rest-api
```

#### Install and run virtual environment
```bash
pip install virtualenv
virtualenv venv
source venv/Scripts/activate
```

#### Install dependencies
Dependencies are found in requirements.txt file:
```bash
pip install Flask Flask-RESTful Flask-JWT Flask-SQLAlchemy
```

#### Run API
```bash
python app.py
```
API will be available from http://localhost:5000/

### Testing API from cli:
#### Register new user
Open up a command prompt and type in the following (note that username and password should be in double quotes):

```bash
curl -d '{"username": [USERNAME], "password": [PASSWORD]}' -H 'Content-Type: application/json' http://localhost:5000/register
```
HTTP/1.1 200 OK
```bash
{"message": "User created successfully."}
```

#### Authenticate user (get access token)
```bash
curl -d '{"username": [USERNAME], "password": [PASSWORD]}' -H 'Content-Type: application/json' http://localhost:5000/auth
```
HTTP/1.1 200 OK
```bash
"access_token": [ACCESS TOKEN]}
```
