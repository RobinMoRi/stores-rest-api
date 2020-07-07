## Simple REST API project using Python Flask

### Acknowledgements

This project is done along with the Udemy course found on the 
following link:
* [REST API Flask and Python](https://www.udemy.com/course/rest-api-flask-and-python/)

The project is done using:
* Flask
* Flask-JWT-Extended
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
#### Logout user (get access token): POST /logout
```bash
curl -d '{"username": [USERNAME], "password": [PASSWORD]}' -H 'Content-Type: application/json' http://localhost:5000/logout
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

#### Get specific item (requires JWT-Extended autorization token): GET /items/<string:name>
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
```bash
# HTTP/1.1 401 Unauthorized
{
  "msg": "Token has expired""
}
```

#### Delete item: DELETE /items/<string:name>
```bash
curl -H "Authorization: Bearer [ACCESS TOKEN]" -X DELETE http://localhost:5000/items/[ITEM NAME]
```
```bash
# HTTP/1.1 200 OK
{
    "message": "Item [ITEM NAME] deleted"
}
```
```bash
# HTTP/1.1 401 Unauthorized
{
    "message": "Admin privilege required"
}
```

#### See all items created GET /items/
```bash
curl -H "Authorization: Bearer [ACCESS TOKEN]" http://localhost:5000/items
```
```bash
# HTTP/1.1 200 OK (If logged in) returns a list of all items (and extra info) collected in the db
{
    "items": [
        {
            "id": [ITEM 1 ID],
            "name": [ITEM 2 NAME],
            "price": [PRICE],
            "store_id": [STORE ID]
        },
        {
            "id": [ITEM 2 ID],
            "name": [ITEM 2 NAME],
            "price": [PRICE],
            "store_id": [STORE ID]
        }
    ]
}

# HTTP/1.1 200 OK (If not logged in) returns a list of just the names of the items in the db
{
    "items": [
        [ITEM NAME 1,
        ITEM NAME 2]
    ],
    "message": "More data available if you log in."
}

```

#### Refresh access token
```bash
curl -H "Authorization: Bearer [REFRESH TOKEN]" -d "{'json': 'mockdata'}" http://localhost:5000/refresh/
```    