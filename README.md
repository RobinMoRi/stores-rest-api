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

### Testing API from cli:

#### Register new user
Open up a command prompt and type in the following (note that username and password should be in double quotes):

```bash
curl -d '{"username": [USERNAME], "password": [PASSWORD]}' -H 'Content-Type: application/json' http://localhost:5000/register
```
HTTP 200 response to POST request:
```bash
{"message": "User created successfully."}
```

#### Authenticate user (get access token)
```bash
curl -d '{"username": [USERNAME], "password": [PASSWORD]}' -H 'Content-Type: application/json' http://localhost:5000/auth
```
HTTP 200 response to POST request:
```bash
"access_token": [ACCESS TOKEN]}
```