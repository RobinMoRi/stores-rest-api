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
#### Register new user: POST /register
Open up a command prompt and type in the following (note that username and password should be in double quotes):

```bash
curl -d '{"username": [USERNAME], "password": [PASSWORD]}' -H 'Content-Type: application/json' http://localhost:5000/register
```

```bash
# HTTP/1.1 201 Created
{
  "message": "User created successfully."
}
```

```bash
# HTTP/1.1 400 Bad Request
{
  "message": "A user with that username already exists"
}
```

#### Authenticate user (get access token): POST /login
```bash
curl -d '{"username": [USERNAME], "password": [PASSWORD]}' -H 'Content-Type: application/json' http://localhost:5000/login
```
```bash
# HTTP/1.1 200 OK
{
    "access_token": [ACCESS TOKEN],
    "refresh_token": [REFRESH TOKEN]
}
```

```bash
# HTTP/1.1 401 Unauthorized
{
    "message": "Invalid credentials"
}
```

#### Create item in store: POST /items/<string:name>
```bash
curl -d '{"price": [PRICE], "store_id": [STORE ID]}' -H 'Content-Type: application/json' http://localhost:5000/items/[ITEM NAME]
```
```bash
# HTTP/1.1 201 Created
{
    "id": [ITEM ID],
    "name": [ITEM NAME],
    "price": [PRICE],
    "store_id": [STORE ID]
}
```

```bash
# HTTP/1.1 400 Bad Request: missing store id
{
    "message": {
        "store_id": "Every item needs a store id"
    }
}
```
```bash
# HTTP/1.1 400 Bad Request: missing price
{
    "message": {
        "price": "This field cannot be left blank"
    }
}
```
```bash
# HTTP/1.1 400 Bad Request
{
    'message': "Item already exists"
}
```
```bash
# HTTP/1.1 404 Not found
{
    'message': 'Item not found'
}
```

#### Get specific item (requires JWT autorization token): GET /items/<string:name>
```bash
curl -H "Authorization: Bearer [ACCESS TOKEN]" http://localhost:5000/items/[ITEM NAME]
```
```bash
# HTTP/1.1 200 OK
{
    "id": [ITEM ID],
    "name": [ITEM NAME],
    "price": [PRICE],
    "store_id": [STORE ID]
}
```
```bash
# HTTP/1.1 422 Unprocessable Entity
{
  "msg": "Signature verification failed"
}
```